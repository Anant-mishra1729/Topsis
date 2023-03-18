# Topsis Score Calculator

<div>
<img src = "https://static.pepy.tech/personalized-badge/topsisanant102003755?period=total&units=international_system&left_color=blue&right_color=grey&left_text=Downloads" width = 120/> 
</div>

## Description
This is a python library for calculating the **Topsis score of a given csv/excel file.** It takes the csv file name, weights vector and impacts vector as input and returns the Topsis score and rank of each row in the csv file.

## Installation

Using package manager [pip](https://pip.pypa.io/en/stable/)  install topsisAnant102003755.
    
```bash
pip install topsisAnant102003755
```


## Usage

* ### Using as python module

#### Input
```python
from topsis.topsis import topsis

# Weights and Impacts are accepted in both list and string format
df = topsis.calculate(
    "sample.csv",
    "0.25,0.25,0.25,0.25",
    "+,+,-,+",
    output_file="output.csv",
    verbose=True,
    force=True,
)

# OR

df = topsis.calculate(
    "sample.csv",
    [0.25, 0.25, 0.25, 0.25],
    ["+", "+", "-", "+"],
    output_file="output.csv",
    verbose=True,
    force=True,
)

```

#### Output
```

Top 5 attributes with highest topsis score:
+-------------------------+-----------------+-----------------+----------+---------+----------------+--------+
| Attribute Or Criteria   |   Price or Cost |   Storage Space |   Camera |   Looks |   Topsis Score |   Rank |
|-------------------------+-----------------+-----------------+----------+---------+----------------+--------|
| Mobile 4                |             275 |              32 |        8 |       4 |         0.796  |      1 |
| Mobile 3                |             300 |              32 |       16 |       4 |         0.5776 |      2 |
| Mobile 1                |             250 |              16 |       12 |       5 |         0.5343 |      3 |
| Mobile 2                |             200 |              16 |        8 |       3 |         0.4224 |      4 |
| Mobile 5                |             225 |              16 |       16 |       2 |         0.0727 |      5 |
+-------------------------+-----------------+-----------------+----------+---------+----------------+--------+

```

* ### Commandline usage

```bash
topsis -i <csv file name> -w=<weights vector> -p=<impacts vector> -o <output file name> -f
```

#### Arguments

* -i, --input: csv file name
* -w, --weights: weights vector
* -p, --impacts: impacts vector
* -o, --output: output file name
* -f, --force: force overwrite of output file

#### Help
    
```bash
$ topsis -h

usage: topsis [-h] -i INPUT [-o OUTPUT] [-w WEIGHTS] [-p IMPACTS] [-f]

Topsis Score Calculator

optional arguments:
  -h, --help            show this help message and exit
  -i INPUT, --input INPUT
                        Input file path in csv or xlsx format
  -o OUTPUT, --output OUTPUT
                        Output file path in csv or xlsx format
  -w WEIGHTS, --weights WEIGHTS
                        Weights separated by comma
  -p IMPACTS, --impacts IMPACTS
                        Impacts separated by comma (either + or -)
  -f, --force           Overwrite output file if it already exists
```

<hr>

## Example

#### sample.csv

A csv file showing data for different mobile handsets having varying features.

| Model  | Storage space(in gb) | Camera(in MP)| Price(in $)  | Looks(out of 5) |
| :----: |:--------------------:|:------------:|:------------:|:---------------:|
| Mobile 1 | 16 | 12 | 250 | 5 |
| Mobile 2 | 16 | 8  | 200 | 3 |
| Mobile 3 | 32 | 16 | 300 | 4 |
| Mobile 4 | 32 | 8  | 275 | 4 |
| Mobile 5 | 16 | 16 | 225 | 2 |

weights vector = [ 0.25 , 0.25 , 0.25 , 0.25 ]

impacts vector = [ + , + , - , + ]

### Input:

```python
topsis -i mydata.csv -w="0.25,0.25,0.25,0.25" -p="+,+,-,+" -o output.csv -f
```

### Output:
```
Weights:  [0.25 0.25 0.25 0.25]
Impacts:  ['+' '+' '-' '+']

Top 5 attributes with highest topsis score:
+-------------------------+-----------------+-----------------+----------+---------+----------------+--------+
| Attribute Or Criteria   |   Price or Cost |   Storage Space |   Camera |   Looks |   Topsis Score |   Rank |
|-------------------------+-----------------+-----------------+----------+---------+----------------+--------|
| Mobile 4                |             275 |              32 |        8 |       4 |         0.796  |      1 |
| Mobile 3                |             300 |              32 |       16 |       4 |         0.5776 |      2 |
| Mobile 1                |             250 |              16 |       12 |       5 |         0.5343 |      3 |
| Mobile 2                |             200 |              16 |        8 |       3 |         0.4224 |      4 |
| Mobile 5                |             225 |              16 |       16 |       2 |         0.0727 |      5 |
+-------------------------+-----------------+-----------------+----------+---------+----------------+--------+

``` 

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License
[MIT](https://choosealicense.com/licenses/mit/)
