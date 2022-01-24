# $group

<br>

Used to group similar items  
<br>

> ### $group does not order its output documents.

<br>

## syntax

    [
        {
            $group: {
                _id: $fieldName
            }
        }
    ]

> ## Output
>
> <br>

    [
        {
            "_id": "Mohali"
        },
        {
            "_id": "CHD"
        },
        {
            "_id": "Kalka"
        }
    ]

> ## if we specify \_id as null or provide no value it will return
>
> <br>

    [
        {
            $group: {
                _id: null
            }
        }
    ]

### Output

    [
        {
            "_id": null
        }
    ]

<br><br>

## To group fields and find total number

<br>

    [
        {
            $group: {
                _id: $fieldName,
                total: {
                    $sum: 1
                }
            }
        }
    ]

> ## Output
>
> <br>

    [
        {
            "_id": "Mohali",
            "total": 2
        },
        {
            "_id": "Kalka",
            "total": 1
        },
        {
            "_id": "CHD",
            "total": 3
        }
    ]

<br><br>

## To group multiple fields:

<br>

    [
        {
            $group: {
                _id: {
                    outputFieldName : '$fieldName',
                    outputFieldName : '$fieldName'
                },
                total: {
                    $sum: 1
                }
            }
        }
    ]


    outputFieldName - name of the field to be displayed in output field

> ## Output
>
> <br>

    [
        {
            "_id": {
                "place": "Mohali",
                "age": 27
            },
            "total": 1
        },
        {
            "_id": {
                "place": "CHD",
                "age": 25
            },
            "total": 2
        },
        {
            "_id": {
                "place": "Mohali",
                "age": 34
            },
            "total": 1
        },
        {
            "_id": {
                "place": "Kalka",
                "age": 43
            },
            "total": 1
        },
        {
            "_id": {
                "place": "CHD",
                "age": 43
            },
            "total": 1
        }
    ]

## To sort on total number

<br>

    [
        {
            $group: {
                _id: {
                    outputFieldName: '$fieldName',
                    outputFieldName: '$fieldName'
                },
                total: {
                    $sum: 1
                }
            }
        }, {
            $sort: {
                total: -1
            }
        }
    ]

> ## Output
>
> <br>

    [
        {
            "_id": {
                "place": "CHD",
                "age": 25
            },
            "total": 2
        },
        {
            "_id": {
                "place": "Mohali",
                "age": 34
            },
            "total": 1
        },
        {
            "_id": {
                "place": "Kalka",
                "age": 43
            },
            "total": 1
        },
        {
            "_id": {
                "place": "CHD",
                "age": 43
            },
            "total": 1
        },
        {
            "_id": {
                "place": "Mohali",
                "age": 27
            },
            "total": 1
        }
    ]

<br><br>

# Summary

<br>

Single Field Group By & Count:

    db.Request.aggregate([
        {"$group" : {_id:"$source", count:{$sum:1}}}
    ])

Multiple Fields Group By & Count:

    db.Request.aggregate([
        {"$group" : {_id:{source:"$source",status:"$status"}, count:{$sum:1}}}
    ])

Multiple Fields Group By & Count with Sort using Field:

    db.Request.aggregate([
        {"$group" : {_id:{source:"$source",status:"$status"}, count:{$sum:1}}},
        {$sort:{"_id.source":1}}
    ])

Multiple Fields Group By & Count with Sort using Count:

    db.Request.aggregate([
        {"$group" : {_id:{source:"$source",status:"$status"}, count:{$sum:1}}},
        {$sort:{"count":-1}}
    ])
