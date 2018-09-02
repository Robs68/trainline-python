# Trainline

[![Travis](https://img.shields.io/travis/tducret/trainline-python.svg)](https://travis-ci.org/tducret/trainline-python)
[![Coveralls github](https://img.shields.io/coveralls/github/tducret/trainline-python.svg)](https://coveralls.io/github/tducret/trainline-python)
[![PyPI](https://img.shields.io/pypi/v/trainline.svg)](https://pypi.org/project/trainline/)
![License](https://img.shields.io/github/license/tducret/trainline-python.svg)

## Description

Non-official Python wrapper and CLI tool for Trainline

# Requirements

- Python 3
- pip3

## Installation

```bash
pip3 install -U trainline
```

## CLI tool usage

```bash
trainline_cli.py --departure="Toulouse" --arrival="Bordeaux" \
--from_date="15/10/2018 08:00" --to_date="15/10/2018 21:00"

trainline_cli.py -d=Toulouse -a=Bordeaux --next=2days
```

Example output :

```bash
departure_date;arrival_date;duration;number_of_segments;price;currency;transportation_mean;bicycle_reservation
15/10/2018 08:19;15/10/2018 10:26;02h07;1;36,0;EUR;train;30,0
15/10/2018 08:19;15/10/2018 10:26;02h07;1;37,5;EUR;train;30,0
15/10/2018 08:19;15/10/2018 10:26;02h07;1;95,5;EUR;train;30,0
[...]
```

## Package usage

```python
# -*- coding: utf-8 -*-
import trainline

results = trainline.search(
	departure_station="Toulouse",
	arrival_station="Bordeaux",
	from_date="15/10/2018 08:00",
	to_date="15/10/2018 21:00")

print(results.csv())
```

Example output :

```bash
departure_date;arrival_date;duration;number_of_segments;price;currency;transportation_mean;bicycle_reservation
15/10/2018 08:00;15/10/2018 10:55;02h55;1;5,0;EUR;coach;unavailable
15/10/2018 08:00;15/10/2018 10:50;02h50;1;4,99;EUR;coach;unavailable
15/10/2018 08:19;15/10/2018 10:26;02h07;1;20,5;EUR;train;10,0
[...]
```

```python
# -*- coding: utf-8 -*-
import trainline

Pierre = trainline.Passenger(birthdate="01/01/1980")
Sophie = trainline.Passenger(birthdate="01/02/1981")
Enzo = trainline.Passenger(birthdate="01/03/2012", cards=[trainline.ENFANT_PLUS])

results = trainline.search(
	passengers=[Pierre, Sophie, Enzo],
	departure_station="Toulouse",
	arrival_station="Bordeaux",
	from_date="15/10/2018 08:00",
	to_date="15/10/2018 21:00",
	bicycle_with_or_without_reservation=True)

print(results.csv())
```

Example output :

```bash
departure_date;arrival_date;duration;number_of_segments;price;currency;transportation_mean;bicycle_reservation
15/10/2018 08:19;15/10/2018 10:26;02h07;1;36,0;EUR;train;30,0
15/10/2018 08:19;15/10/2018 10:26;02h07;1;37,5;EUR;train;30,0
15/10/2018 08:19;15/10/2018 10:26;02h07;1;95,5;EUR;train;30,0
[...]
```

# TODO

- [X] Implement `get_station_id`
- [X] Implement the use of passengers during search
- [ ] Create a sort function in Trips class (to get the cheapest trips first for example)
- [ ] Add filter for class (first, second), for max_duration
- [X] Calculate total price with bicycle reservation if search 'with_bicyle' (and export it in csv)
- [X] Calculate total price for all the passengers (and export it in csv) => may need to create a class for Folder 
- [ ] Create the CLI tool and update README
