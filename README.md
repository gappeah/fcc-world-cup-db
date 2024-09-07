# World Cup Database

This project is part of the FreeCodeCamp Relational Database certification. The objective was to build a PostgreSQL database to store World Cup match results and create a set of Bash scripts to insert data into the database and retrieve meaningful information.

## Project Structure

- **Database**: The database is managed using PostgreSQL.
- **Scripts**: Bash scripts (`insert_data.sh` and `queries.sh`) were created to insert match data into the database and query the database for specific insights.

### Files

- `worldcup.sql`: Contains SQL commands to create the database, including tables for teams and games.
- `games.csv`: A CSV file containing match data from the 2014 and 2018 World Cup tournaments.
- `insert_data.sh`: A Bash script to insert data from `games.csv` into the database.
- `queries.sh`: A Bash script to query the database and retrieve specific information.

## Database Schema

The database consists of the following tables:

### `teams` Table

| Column Name | Data Type  | Constraints      |
| ----------- | ---------- | ---------------- |
| `team_id`   | SERIAL     | PRIMARY KEY      |
| `name`      | VARCHAR(255) | UNIQUE, NOT NULL |

### `games` Table

| Column Name      | Data Type  | Constraints                           |
| ---------------- | ---------- | ------------------------------------- |
| `game_id`        | SERIAL     | PRIMARY KEY                           |
| `year`           | INTEGER    | NOT NULL                              |
| `round`          | VARCHAR(255) | NOT NULL                              |
| `winner_goals`   | INTEGER    | NOT NULL                              |
| `opponent_goals` | INTEGER    | NOT NULL                              |
| `winner_id`      | INTEGER    | REFERENCES `teams(team_id)`            |
| `opponent_id`    | INTEGER    | REFERENCES `teams(team_id)`            |

## Usage

### Prerequisites

- **PostgreSQL**: Ensure PostgreSQL is installed and running on your machine. Connect to the database using:

  ```bash
  psql --username=freecodecamp --dbname=worldcup
  ```

- **Database Setup**: The database should be created and populated using the provided `worldcup.sql` and `games.csv` files.

### Running the Script

#### Insert Data into the Database

To insert data from the `games.csv` file into the database, run the `insert_data.sh` script:

```bash
./insert_data.sh
```

This script will read the match data from `games.csv` and insert it into the `teams` and `games` tables. It will also ensure that teams are added only once.

#### Query the Database

To query the database and retrieve various statistics about the World Cup matches, run the `queries.sh` script:

```bash
./queries.sh
```

This script retrieves the following data:

- Total number of goals scored by winning teams.
- Total number of goals scored in all games by both teams.
- Average number of goals by winning teams.
- Average number of goals by both teams.
- Most goals scored in a single game by one team.
- Number of games where the winning team scored more than two goals.
- The winner of the 2018 World Cup.
- Teams that played in the 2014 'Eighth-Final' round.
- Unique winning team names in the dataset.
- Year and team name of all the champions.
- Teams that start with 'Co'.

### Example Output

```bash
Total number of goals in all games from winning teams:
68

Total number of goals in all games from both teams combined:
90

Average number of goals in all games from the winning teams:
2.1250000000000000

Average number of goals in all games from the winning teams rounded to two decimal places:
2.13

Average number of goals in all games from both teams:
2.8125000000000000

Most goals scored in a single game by one team:
7

Number of games where the winning team scored more than two goals:
6

Winner of the 2018 tournament team name:
France

List of teams who played in the 2014 'Eighth-Final' round:
Algeria
Argentina
Belgium
Brazil
Chile
Colombia
Costa Rica
France
Germany
Greece
Mexico
Netherlands
Nigeria
Switzerland
United States
Uruguay

List of unique winning team names in the whole data set:
Argentina
Belgium
Brazil
Colombia
Costa Rica
Croatia
England
France
Germany
Netherlands
Russia
Sweden
Uruguay

Year and team name of all the champions:
2014|Germany
2018|France

List of teams that start with 'Co':
Colombia
Costa Rica
```

### Error Handling

- If a team does not exist in the database, it will be inserted during the data insertion process.
- The scripts ensure that no duplicate team entries are made in the `teams` table.

## Project Completion

### Database Fixes

The database was refined to meet the project requirements:

1. The `teams` table stores unique team names.
2. The `games` table links teams with their match outcomes, ensuring referential integrity between teams and games.

### Git Repository

The project folder was initialized as a Git repository:

```bash
git init
```

The repository was ensured to have a `main` branch with at least five commits, using conventional prefixes like `fix:`, `feat:`, `refactor:`, etc.

## Installation

1. Clone this repository.
2. Set up the database:
   - Log in to PostgreSQL:
     ```bash
     psql --username=freecodecamp --dbname=postgres
     ```
   - Run the SQL commands in `worldcup.sql` to create and populate the database:
     ```sql
     \i worldcup.sql
     ```
3. Make sure the `insert_data.sh` and `queries.sh` scripts have execution permissions:
   ```bash
   chmod +x insert_data.sh queries.sh
   ```

4. Run the scripts as described above.