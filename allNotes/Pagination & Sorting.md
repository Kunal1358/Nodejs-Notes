## Pagination & Sorting

    let page = parseInt(req.query.page) || 1;
    let limit = parseInt(req.query.size) || 10;
    let skip = (page - 1) * limit;
    let sortBy = req.query.sort || "createdAt";
    let sort = {}
    sort.sortBy = sortBy
    const sortType = req.query.sortType && req.query.sortType === 'asc' ? 1 : req.query.sortType && req.query.sortType === 'desc' ? -1 : -1;

 </br>

    .sort(sort)
    .skip(skip)
    .limit(limit)
    .lean()

 </br>

## Aggregation

    const page = +parseInt(req.query.page) || 1;
    const sortBy = req.query.sort || "createdAt";
    const ITEM_PER_PAGE = +parseInt(req.query.size) || 10;
    const sortType = req.query.sortType && req.query.sortType === 'asc' ? 1 : req.query.sortType && req.query.sortType === 'desc' ? -1 : -1;

 </br>

      pipeline.push(
        { $sort: { [sortBy]: sortType } },
        { $skip: (page - 1) * ITEM_PER_PAGE },
        { $limit: ITEM_PER_PAGE }
      )
