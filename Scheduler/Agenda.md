# [Agenda](https://www.npmjs.com/package/agenda#repeateveryinterval-options)

Code

    const Agenda = require('agenda');
    const dbURL = 'mongodb://127.0.0.1:27017/agendajs';

    // configure agenda
    const agenda = new Agenda({
        db: { address: dbURL, collection: 'Agenda' },
        processEvery: '1 seconds',
        useUnifiedTopology: true
    });

    // Defining a job
    agenda.define('log hello medium', async job => {

        console.log('Job started')
        const { data } = job.attrs;

        job.priority("highest");
        await job.save();

        console.log(`Hello ${data.name} 👋`);

    });

    //Calling Job
    (async function () {
        await agenda.start(); // Start Agenda instance

        await agenda.every('1 seconds', 'log hello medium', { name: 'NodeJs', age: '100', description: 'null' });

        // await agenda.schedule('in 1 minute', 'log hello medium', { name: 'NodeJs', age: '100', description: 'null' });
    })();
