# Word Sequence Finder

## Description
This is a dotnet 5.0 console app that reads text, and prints out 100 most common words in descending order. This text can be passed to the application as a file parameter (or multiple), or via stdin. 

## How to run
[Install dotnet 5.0, click here!](https://dotnet.microsoft.com/download)

### Commands
Run these commands in this directory:

```
dotnet build
```

to test:
```
dotnet test
```

to run:
```
dotnet run ./texts/moby-dick.txt ./texts/brothers-karamazov.txt
cat ./texts/moby-dick.txt  | dotnet run
```

## How this works

This app processes all input into one string, modifies string to remove punctuation, make lowercase, etc. Then goes through that entire string, processing 3 word sequences and adding them to a dictionary. This dictionary is sorted by descending value at the end, and then read from to produce the output.

This should handle unicode correctly, and removes punctuation such that `whale-men` becomes `whalemen` and `whale’s` becomes `whales`
## Improvements

We could break input text into multiple chunks, and process all those chunks into the dictionary simultaneously taking advantage of multiple threads.

Add more tests

Logs / error handling

## Execution Time

### Passing in file name:

```
145 ms moby dick
90 ms bros
208 ms both
```
### stdin:
```
269 ms moby dick
````

## Bonus Docker

to run locally, pull in from docker public repo
 ```
docker run -it --rm aidanhl/word-sequence-finder
docker run -it --rm aidanhl/word-sequence-finder "/moby-dick.txt"
docker run -it --rm word-sequence-finder "/brothers-karamazov.txt"
docker run -it --rm word-sequence-finder "/brothers-karamazov.txt" "/moby-dick.txt"
```

to build ` docker build -t aidanhl/word-sequence-finder -f Dockerfile .`
### What this does
This is a basic docker app, we just mount the two text sample documents inside the docker container, and default to running moby-dick. We allow the user to specify "/brothers-karamazov.txt" or both if desired. This can be improved by allowing users to mount and use a text file of their choice, or pipe in user input to stdin of the application.
