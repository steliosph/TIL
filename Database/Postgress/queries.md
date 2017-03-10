When wanting to insert into the database multiple entries that have the same keywe can use the unnest function as follow

```
INSERT INTO list_people (list_id,people_id)
SELECT 1, x
FROM unnest (ARRAY [86872,302675,328998,6537,51150,319177]) x 
```
