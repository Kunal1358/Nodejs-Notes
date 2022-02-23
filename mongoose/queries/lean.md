
    const leanDoc = await MyModel.findOne().lean();


lean option tells Mongoose to skip instantiating a full Mongoose document and just give you the POJO.


Lean and Populate
Populate works with lean(). If you use both populate() and lean(), the lean option propagates to the populated documents as well.
In the below example, both the top-level 'Group' documents and the populated 'Person' documents will be lean.

Virtual populate also works with lean.

When to Use Lean
If you're executing a query and sending the results without modification to, say, an Express response, you should use lean. 
In general, if you do not modify the query results and do not use custom getters, you should use lean(). 
If you modify the query results or rely on features like getters or transforms, you should not use lean().
