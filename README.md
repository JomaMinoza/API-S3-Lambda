# Pre requirements

- npm
- python 3.6, virtualenv
- AWS credentials configured
- serverless toolkit (`npm install -g serverless`)

# Installation


```bash
git clone https://github.com/quentinf00/API-S3-Lambda.git
cd API-S3-Lambda

virtualenv venv  — python=python3.6
source venv/bin/activate

yarn install
pip install -r requirements.txt

sls invoke local -f init_athena_schema
sls deploy
```

# Usage

```bash
export ENDPOINT=FILL_WITH_THE_ENDPOINT_GENERATED_DURING_THE_DEPLOYMENT # e.g https://....amazonaws.com/dev
# list all users
curl -X GET $ENDPOINT/user/list

# Create a new user
curl -X POST $ENDPOINT/user
  -d '{
"first_name": "Hello",
"last_name": "Z",
"birthday": "2018-01-01"
}'

export USER_ID=FILL_WITH_THE_ID_RETURNED_BY_THE_POST
# Get the existing user
curl -X GET $ENDPOINT/user/$USER_ID
  
# Modify the existing user
curl -X PUT $ENDPOINT/user/$USER_ID \
  -d '{
"first_name": "toto",
"last_name": "titi",
"birthday": "2018-01-01"
}'

# Delete the existing user
curl -X DELETE $ENDPOINT/user/$USER_ID
```