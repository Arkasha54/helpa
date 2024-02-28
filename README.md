# helpa
```
UPDATE Users SET [image] = (SELECT * FROM OPENROWSET(BULK N'C:\Users\nasik\Pictures\ff961525.jpg', SINGLE_BLOB) AS image)WHERE ID = 1
```
