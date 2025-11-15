# Boston Metro Simulator

A C++ simulation of a metro train system that models passengers boarding, riding, and departing trains across multiple stations along a route.

## Overview

The Boston Metro Simulator is an object-oriented program that simulates the operation of a metro train line. The train travels through a series of stations, picking up and dropping off passengers as it moves along its route. Each passenger has a departure station, and the simulator tracks all passengers from boarding to departure.

## Features

- **Train Movement**: Simulates a train moving through a series of stations in a continuous loop
- **Passenger Management**: Tracks passengers waiting at stations and riding on the train
- **Queue-Based System**: Uses queue data structures to manage passenger ordering
- **Flexible Input**: Accepts station lists and command files or interactive input
- **Output Logging**: Records all passenger departures to an output file

## Project Structure

```
Boston_Metro/
├── main.cpp              # Program entry point and command-line handling
├── MetroSim.h            # MetroSim class interface
├── MetroSim.cpp          # MetroSim class implementation
├── PassengerQueue.h      # PassengerQueue class interface
├── PassengerQueue.cpp    # PassengerQueue class implementation
├── Passenger.h           # Passenger struct definition
├── Passenger.cpp         # Passenger struct implementation
├── Makefile              # Build configuration
├── stations.txt          # Example station file
├── test_commands.txt     # Example commands file
└── unit_tests.h          # Unit testing framework
```

### Core Components

**MetroSim**: Main simulation controller that manages the train, stations, and passenger flow.

**PassengerQueue**: Queue data structure for managing passengers in FIFO order at stations and on trains.

**Passenger**: Data structure representing a passenger with an ID, arrival station, and destination station.

**Station**: Structure containing a station name, number, and passenger queue.

## Compilation

Compile the program using the provided Makefile:

```bash
make MetroSim
```

This will create the `MetroSim` executable.

To clean up object files and executables:

```bash
make clean
```

## Usage

The program can be run in two modes:

### Interactive Mode

```bash
./MetroSim <stationsFile> <outputFile>
```

Commands are entered via standard input (keyboard).

### File-Based Mode

```bash
./MetroSim <stationsFile> <outputFile> <commandsFile>
```

Commands are read from the specified commands file.

### Arguments

- `stationsFile`: Text file containing the list of station names (one per line)
- `outputFile`: File where passenger departure records will be written
- `commandsFile`: (Optional) File containing simulation commands

## Input File Formats

### Stations File

A plain text file with one station name per line:

```
Heath St
Back of the Hill
Riverway
Mission Park
...
```

Stations are numbered starting from 0 in the order they appear.

### Commands File

A text file containing simulation commands (one per line):

```
m m
p 1 5
m m
p 2 7
m f
```

## Commands

The simulator accepts the following commands:

- **`m m`** - Move Metro: Advances the train to the next station
  - Passengers exit at their destination station
  - Waiting passengers board the train
  - Station number wraps around to 0 after the last station

- **`p <arrival> <departure>`** - Add Passenger: Adds a new passenger
  - `<arrival>`: Station number where passenger appears (0-indexed)
  - `<departure>`: Station number where passenger wants to exit (0-indexed)
  - Passenger receives a unique ID and joins the queue at the arrival station

- **`m f`** - Metro Finish: Ends the simulation and exits the program

