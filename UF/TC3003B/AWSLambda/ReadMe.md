# AWSLambda

This tutorial shows how to create a API with python backbone, steps:
1. Create a Lambda function
2. Create an API gateway
3. Test using curl

## Lambda Function
1. Login https://us-east-1.console.aws.amazon.com/console/
2. Search Lambda
3. Create function
4. Select Author from scratch
5. Give funcion name, e.g., _myfunction_
6. Select Runtime python 3.8
7. Leave the rest and click on create Function

8. Edit _lambda_function.py_ as
```python
# lambda_function.py
import json
def lambda_handler(event, context):
    Body = event.get('body')
    Body = json.loads(Body)
    Time = Body.get('time')
    return {
        'statusCode': 200,
        'body': json.dumps('Hello you ! %s' %(Time) )
    }
```

## API gateway
1. Login https://us-east-1.console.aws.amazon.com/console/
2. Search API gateway
3. Click on Create API
4. Select HTTP API and click Build
5. Add integration, select Lambda
6. Find _myfunction_
7. Click on add integration
8. Name API, e.g., newAPI
9. Methods, leave ANY, click Next
10. Stages default and click Next
11. Review, click Create
12. Copy *Invoke URL*, e.g., https://{APIgate}.execute-api.{zone}.amazonaws.com/

## Curl
Generate the following bash script and save it, e.g., mybash.sh
```bash
curl -X POST \
  'https://{APIgate}.execute-api.{zone}.amazonaws.com/{myfunction}' \
  -H 'content-type: application/json' \
  -H 'day: Thursday' \
  -d '{"time":"sunrise"}' 
```
Run your bash
```bash
bash mybash.sh
```

