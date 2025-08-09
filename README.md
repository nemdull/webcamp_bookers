# WebCamp Bookers Application

This is a Ruby on Rails application, likely designed for booking services or resources.

## Technologies

- Ruby on Rails
- Ruby
- JavaScript

## Setup and Installation

1. Clone the repository:
   ```bash
   git clone git@github.com:nemdull/webcamp_bookers.git
   cd webcamp_bookers
   ```
2. Install Ruby dependencies:
   ```bash
   bundle install
   ```
3. Install JavaScript dependencies (if any, check `package.json`):
   ```bash
   yarn install # or npm install
   ```
4. Database setup:
   ```bash
   rails db:create
   rails db:migrate
   # rails db:seed (if seed data is available)
   ```
5. Run the application:
   ```bash
   rails s
   ```

## How to Run Tests

```bash
rails test
```