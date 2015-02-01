# https-github.com-rdpeng-ProgrammingAssignment2-3amhh2009amhh2013mdjhh2013rrhs1984mlhh19


 numeric vector and caches its mean.

The first function,  makeVector  creates a special "vector", which is really a list containing a function to
1. set the value of the vector
2. get the value of the vector
3. set the value of the mean
4. get the value of the mean
> makeVector <- function(x = numeric()) {
        m <- NULL
        print(environment())
        evn <- environment()
        print(parent.env(evn))
        set <- function(y) {
                x <<- y
                m <<- NULL
        }
        get <- function() x
        setmean <- function(mean) m <<- mean
        getmean <- function() m
        getevn<- function() environment()
        list(set = set, get = get,
             setmean = setmean,
             getmean = getmean,
             getevn = getevn)
 }
 now lets assign this function to a variable vec
> x <- 1:10000
> vec<-makeVector(x)
<environment: 0x2924c28>
<environment: R_GlobalEnv>
> vec$getmean()

NULL
> mx <- mean(x)
> vec$setmean(mx)
> vec$getmean()
[1] 5000.5

> vec$getevn()
<environment: 0x353b260>
> ls(vec$getevn())
character(0)

> parent.env(vec$getevn())
<environment: 0x3322ab8>
> ls(parent.env(vec$getevn()))
[1] "evn"     "get"     "getevn"  "getmean" "m"       "set"     "setmean"
[8] "x"

> parent.env(vec$getevn())$m
[1] 5000.5

cachemean <- function(x, ...) {

    

    start_time <- Sys.time()

    

    m <- x$getmean()

    if(!is.null(m)) {

        message("getting cached data")

    

        end_time <- Sys.time()

        time_duration <- end_time - start_time

        print(time_duration)

        

        return(m)

    }

    data <- x$get()

    m <- mean(data, ...)

    x$setmean(m)

    

    end_time <- Sys.time()

    time_duration <- end_time - start_time

    print(time_duration)

    

    m

}

> cachemean(mean.methods)
Time difference of 0.002012968 secs
 [1] 500000.5

 

Running it a second time we get:

 

> cachemean(mean.methods)
getting cached data
 Time difference of 0 secs
 [1] 500000.5





