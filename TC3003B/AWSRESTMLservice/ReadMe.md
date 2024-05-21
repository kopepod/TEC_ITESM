# AWS REST ML service

This code is to generate a Machine Learning REST service using AWS

1. Set Environment
2. Create a Lambda function
3. Create an API gateway
4. Test using curl

## Set Environment
```bash
conda create -n test python=3.8
pip install scikit-learn==0.22.1 numpy==1.19.5 pandas==1.2.5
```

## Lambda Function
1. Login https://us-east-1.console.aws.amazon.com/console/
2. Search Lambda
3. Create function
4. Select Author from scratch
5. Give funcion name, e.g., _myfunction_
6. Select Runtime python 3.8
7. Leave the rest and click on create Function
8. Generate BestModel.p as https://github.com/kopepod/BestModel
8. Edit _lambda_function.py_ as
```python
# lambda_function.py
import json
import pickle
import numpy

model = pickle.load( open( "BestModel.p", "rb" ) )

def lambda_handler(event, context):
	Body = event.get('body')
	Body = json.loads(Body)
	x = Body.get('x')
  
	x= numpy.fromstring(x, dtype = float, sep = ',')
  
	y_hat = model.predict(x.reshape(1,-1))

	label = model.Classes[y_hat[0]]
    
	return {
		'statusCode': 200,
		'body': json.dumps('Label:%s' %(label))
	}
```
9. zip lambda_function.py and BestModel.p into myzip.zp
10. upload myzip.zip from AWS lambda
11. Add layers (scroll down Add a Layer)
* python-3-8-scikit-learn-0-22-1 select your region https://github.com/model-zoo/scikit-learn-lambda/blob/master/layers.csv

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
  -d '{"x":"4.4,3.5,5.5,4.6"}' 
```
Run your bash
```bash
bash mybash.sh
```
