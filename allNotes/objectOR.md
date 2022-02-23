    let qry = {
        _id: {
            id: "1"
        },
        isDelete: false,
    }
        let or = []
    or.push({ name: 'Kunal' })

# Before

    { \_id: { id: '1' }, isDelete: false }
    [ { name: 'Kunal' } ]

# Query

## qry.or = or;

    { \_id: { id: '1' }, isDelete: false, or: [ { name: 'Kunal' } ] }
    [ { name: 'Kunal' } ]

## qry.$or = or;

    { _id: { id: '1' }, isDelete: false, '$or': [ { name: 'Kunal' } ] }
    [ { name: 'Kunal' } ]
