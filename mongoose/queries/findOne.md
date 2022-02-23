    const lrn = await learnIndex.findOne({ name: 'jkKzN' }, {
        age: 1,
        name:1
    })
    
    1st stage is query to be found
    2nd stage is projections (fields to be projected)
    3rd stage is options - https://mongoosejs.com/docs/api.html#query_Query-setOptions
    4th stage is callback which is optional 
