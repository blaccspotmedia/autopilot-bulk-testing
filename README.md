# ta-bulk-testing
This cli helps with bulk tests to the Autopilot infraestructure. It uses csv file fixtures as input and returns a json report if needed.

## Installing
`npm install -g ta-bulk-testing`

## Twilio's config parameters
In order for this application to run, it requires you to set three twilio variables.

How to get them?:
- Auth Token: <a href="https://www.twilio.com/console">here</a>
- Account SID: <a href="https://www.twilio.com/console">here</a>
- Assistant SID: <a href="https://www.twilio.com/console/autopilot/list">here</a>

There are three ways that the cli will try to get those variables from:
1. The `Environment variables` given by the OS, with the names of `ACCOUNT_SID`, `AUTH_TOKEN` and `ASSISTANT_SID`.
2. The cli parametes as `account_sid`, `auth_token`, `assistant_sid`.
3. A file generated by `twilio autopilot cli` which is located in ~/.twilio/config.json.

If any of those three places have the variables, it will raise an exception instead of running.

## Running
Now you're able to run the project in the cli.
```
This is a cli program that helps you make bulk testing to
twilio\'s autopilot infraestructure. It uses a csv file fixtures
as input and returns a json report if needed.

Usage
  $ ta-bulk-testing <action>

Options
    --expand, -e Take the fixtures file and expand it.
                 This process relies on "intent-utterance-expander"
                 project.
    --export, -x Export report to a given name.
                 Eg. --export report.json.
                 If you send 'export' without a filename,
                 it will output the report in output.json.
    --fixtures, -f Import an specific fixture file. CSV Format
                   is mandatory.
    --language, -l Language for the testing. Default: 'en-US'
    --account_sid, -s Twilio's account SID, default will try to
                      lookup for it in ~/.twilio/config.json.
    --auth_token, -t Twilio's authorization token, default will
                     try to lookup for it in ~/.twilio/config.json.
    --assistant_sid, -a Twilio's specific assistant ID for this testing.

Examples
  $ ta-bulk-testing --expand --fixtures ./fixtures/en-US.csv --export
```

## Fixtures
In order to generate the fixtures, this project relies on <a href="https://www.npmjs.com/package/intent-utterance-expander">Intent Utterance Expander</a> in order to expand the samples in your file. The first row, should be `task, intent` so that the library can match correctly the sample to the task that the bot should respond.

### Example of the fixture file using the expander:
```csv
task, samples
hello_world, (Hi | Hello | Hey) I am Erick
```

### Example of the fixture file without using the expander:
```csv
task, samples
hello_world, Hi I am Erick
hello_world, Hello I am Erick
hello_world, Hey I am Erick
hello_world, Hey I am Erick
```
**Note:** It's suggested that you use the expander to minimize the size of your fixture file.

In the folder `fixtures` of this project, there's an example `.csv` file using the expander feature.

## Development
### Installation
In order to install it, just clone the project and install the dependencies.
1. `git clone <repo>`
2. `yarn install # I'm using yarn, but you can you npm to install the dependencies.`

### Configuration
In order to be able to run this project, you'll need to have an `.env` file with your credentials.
1. `cp .env.example .env`
2. Fill your `ACCOUNT_SID`, `AUTHO_TOKEN` and `ASSISTANT_SID`.

## TODO
- [ ] Refactor the code to receive the twilio's variables from the command.
- [ ] Add testing
