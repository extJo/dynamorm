---
id: streaming
title: Streaming (CDC)
sidebar_label: Streaming (CDC)
---

## Intro
[DynamoDB Stream](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Streams.html) is simple yet elegantly powerful tool for capturing data changes in DynamoDB  
in general, any processes that should happen reactively based on data change (insert / delete / update) of DynamoDB, can be implemented with DynamoDB Stream.  
this can be used for a lot of things, such as  
- Sending notification based on model change. Message record inserted => send notification.
- [backup records when it's expired by TTL](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/time-to-live-ttl-streams.html)
- Asynchronously update counters / stats. Like created => post.like_count += 1

And more.  


Most of those features are also implmentable in periodic batch reading, but streaming is far more superior on those aspects:  
1. Efficient data reading & indexing
   1. You don't need to create new index such as "updated_at" just to get the list of items has been updated
2. Fail safe retrying
   1. DynamoDB Stream 

| Entity                   | Data Structure                               |
| :---                     |  :---                                        |
| [HashPrimaryKey](#hashprimarykey)           | Hash                                         |
| [FullPrimaryKey](#fullprimarykey)           | Hash + Range                                 |
| [LocalSecondaryIndex](#localsecondaryindex)      | Hash (Same with PK) + Range                  |
| [HashGlobalSecondaryIndex](#hashglobalsecondaryindex) | Hash (Can be different with PK)              |
| [FullGlobalSecondaryIndex](#fullglobalsecondaryindex) | Hash + Range (both can be different with PK) |

So for example, **FullPrimaryKey** and **FullGlobalSecondaryIndex** has almost identical query interface, except few APIs


## HashPrimaryKey
### ```.get(hashKey: HashKeyType, options: { consistent: boolean }): Promise<T | null>```
find single record with hashKey, return null if record not exists  
if the record is < 4KB, consumes 1 read capacity.
### ```.scan(options)```
(TBD)

### ```.batchGet(hashKeys)```
(TBD)

### ```.batchGetFull()```
(TBD)

## FullPrimaryKey
### ```.get(hashKey, sortKey, options)```
(TBD)

### ```.batchGet(keys)```
(TBD)

### ```.batchGetFull(keys)```
(TBD)

### ```.query(options)```
(TBD)

### ```.scan(options)```
(TBD)

## LocalSecondaryIndex
Identical to [FullPrimaryKey](#fullprimarykey)

## HashGlobalSecondaryIndex
Identical to [HashPrimaryKey](#hashprimarykey)

## FullGlobalSecondaryIndex
Identical to [FullPrimaryKey](#fullprimarykey)

<!-- ### .delete(hashKey, sortKey)
### .update(hashKey, sortKey, changes)
### .batchDelete(keys) -->
<!-- #### .delete(hashKey)
#### .batchDelete(hashKeys)
#### .update(hashKey, changes) -->