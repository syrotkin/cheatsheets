## Subset - create a new dataframe

```R
minwageNJ <- subset(minwage, subset = (location != "PA"))
head(minwageNJ)
```

### Another way to subset:

```R
minwage[minwage$location != "PA",] 
```

Remember the comma: you can use it to select columns