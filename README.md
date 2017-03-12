# pandas to pyspark

    from pyspark.sql import functions as F

Use `.collect(), .take(5), .toPandas()` etc to evaluate and pull results to local session.

<table>
    <tr> <th>pandas</th><th>pyspark</th><th>desc</th> </tr>
    <tr>
        <td>df['a'].unique()</td>
        <td>
            df.select('a').distinct()
            df.select('a').distinct().rdd.map(lambda x: x['a'])
        </td>
	      <td></td>
    </tr>
    <tr>
        <td>df['a'].value_counts()</td>
        <td>df.groupby('a').count()</td>
        <td></td>
    </tr>
    <tr>
        <td>df.groupby(['a', 'b'])['c'].first()</td>
        <td>df.groupby(['a', 'b']).agg(F.first('c'))</td>
        <td></td>
    </tr>
    <tr>
        <td>df['a'] = 0</td>
        <td>df = df.withColumn('a', F.lit(0))</td>
        <td></td>
    </tr>
    <tr>
        <td>df['b'] = df['a'] + 1</td>
        <td>df = df.withColumn('b', df['a'] + 1
        )</td>
        <td></td>
    </tr>
    <tr>
        <td>df[['a', 'b', 'c']].set_index(['a', 'b'])['c'].sort_index().unstack(['b']).fillna(method='ffill')</td>
        <td></td>
        <td></td>
    </tr>
</table>

# Misc

Dump of pyspark Dataframe `__dir__`:

    pdf = pd.DataFrame.from_items([('A', [1, 2, 3]), ('B', [4, 5, 6])])
    sdf = sqlCtx.createDataFrame([(1, 4), (2, 5), (3, 6)], ["A", "B"])

    print('\n'.join(sorted([x for x in sdf.__dir__() if not x.startswith('_')])))
    agg
    alias
    approxQuantile
    cache
    checkpoint
    coalesce
    collect
    columns
    corr
    count
    cov
    createGlobalTempView
    createOrReplaceTempView
    createTempView
    crossJoin
    crosstab
    cube
    describe
    distinct
    drop
    dropDuplicates
    drop_duplicates
    dropna
    dtypes
    explain
    fillna
    filter
    first
    foreach
    foreachPartition
    freqItems
    groupBy
    groupby
    head
    intersect
    isLocal
    isStreaming
    is_cached
    join
    limit
    na
    orderBy
    persist
    printSchema
    randomSplit
    rdd
    registerTempTable
    repartition
    replace
    rollup
    sample
    sampleBy
    schema
    select
    selectExpr
    show
    sort
    sortWithinPartitions
    sql_ctx
    stat
    storageLevel
    subtract
    take
    toDF
    toJSON
    toLocalIterator
    toPandas
    union
    unionAll
    unpersist
    where
    withColumn
    withColumnRenamed
    withWatermark
    write
    writeStream