## Subset - create a new dataframe

```R
minwageNJ <- subset(minwage, subset = (location != "PA"))
head(minwageNJ)
```

You can also select columns:
```R
subset(airquality, Temp > 80, select = c(Ozone, Temp))
```


### Another way to subset:

```R
minwage[minwage$location != "PA",] 
```

Remember the comma: you can use it to select columns