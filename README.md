# Topsis Score Calculator

<div>
<a href = "https://pepy.tech/project/topsisanant102003755/"><img src = "https://static.pepy.tech/personalized-badge/topsisanant102003755?period=total&units=none&left_color=black&right_color=orange&left_text=Downloads" width = 115/></a>&nbsp;
<a href = "https://pypi.org/project/topsisAnant102003755/"><img alt="PyPI" src="https://img.shields.io/pypi/v/topsisanant102003755" width = 80></a>
</div>

## Description
This is a python library for calculating the **Topsis score of a given csv/excel file.** It takes the csv file name, weights vector and impacts vector as input and returns the Topsis score and rank of each row in the csv file.

## Installation 
### Using pip ([PyPI](https://pypi.org/project/topsisAnant102003755/))
    
```sh
pip install topsisAnant102003755
```
### Using releases .whl
* Download ```topsisAnant102003755-1.2-py3-none-any.whl``` from releases
* Create separate python environment to avoid package conflicts
```sh
python -m venv env
source /env/activate
python install topsisAnant102003755-1.2-py3-none-any.whl
```


## Usage

#### sample.csv

A csv file showing data for different mobile handsets having varying features

| Model  | Storage space (in GB) | Camera (in MP)| Price (in $)  | Looks (out of 5) |
| :----: |:--------------------:|:------------:|:------------:|:---------------:|
| Mobile 1 | 16 | 12 | 250 | 5 |
| Mobile 2 | 16 | 8  | 200 | 3 |
| Mobile 3 | 32 | 16 | 300 | 4 |
| Mobile 4 | 32 | 8  | 275 | 4 |
| Mobile 5 | 16 | 16 | 225 | 2 |

we want to select best mobile phone according to our needs
|  | Storage space (in GB) | Camera (in MP)| Price (in $)  | Looks (out of 5) |
|:---------:|:--------------------:|:------------:|:------------:|:---------------:|
| Weights (Importance) | 0.25 | 0.25 | 0.25 | 0.25 |
| Impact (Increase/Decrease value) | + | + | - | + |


```python
weights = [ 0.25 , 0.25 , 0.25 , 0.25 ]
impacts = [ + , + , - , + ]
```

* ### Commandline usage

```bash
topsis -i <csv file name> -w=<weights vector> -p=<impacts vector> -o <output file name> -f
```

#### Arguments
```sh
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

#### Input

```python
topsis -i mydata.csv -w="0.25,0.25,0.25,0.25" -p="+,+,-,+" -o output.csv -f
```
   


#### Output
```md
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

* ### Python module

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
```md

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
MIT
