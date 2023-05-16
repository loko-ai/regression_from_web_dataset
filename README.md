<html><p><a href="https://loko-ai.com/" target="_blank" rel="noopener"> <img style="vertical-align: middle;" src="https://user-images.githubusercontent.com/30443495/196493267-c328669c-10af-4670-bbfa-e3029e7fb874.png" width="8%" align="left" /> </a></p>
<h1>Regression from web dataset</h1><br></html>

A simple example of training/predicting a regression model using the **Predictor** and **HTTP Request** component.

From the **Projects** tab, click on **Import from git** and copy and paste the URL of the current page 
(i.e. https://github.com/loko-ai/regression_from_web_dataset):
<p align="center"><img src="https://user-images.githubusercontent.com/30443495/230620716-c67e5e58-b71e-4817-9213-39a7e0e9cddd.gif" width="80%" /></p>


### STEP1: Model training

The diabetes dataset has the following features:

`age:` age in years

`sex:` sex

`bmi:` body mass index

`bp:` average blood pressure

`s1:` tc, total serum cholesterol

`s2:` ldl, low-density lipoproteins

`s3:` hdl, high-density lipoproteins

`s4:` thc, total cholesterol / HDL

`s5:` ltg, possibly log of serum triglycerides level

`s6:` glu, blood sugar level

`target:` quantitative measure of disease progression one year after baseline

In order to predict the target feature, we're going to use a liner regression, a LASSO model (Least Absolute Shrinkage and 
Selection Operator).

You have to create a new predictor from the **Predictors** tab using the **Advanced** section. You've to select the 
*regression* task and then the *sk.Lasso* model: 

<p align="center"><img src="https://user-images.githubusercontent.com/30443495/231183804-ea048646-a957-4d57-9d3a-fc9ec230ff3c.gif" width="80%" /></p>

In order to start the project remember to press the play button on the right of the project's name:

<p align="center"><img src="https://github.com/Cecinamo/ner/assets/30443495/2a50618e-750c-4e1f-a961-f6d3dc1af912" width="80%" /></p>

Then you can fit the diabetes model:

<p align="center"><img src="https://user-images.githubusercontent.com/30443495/231186287-2b2294de-bc2f-42c4-8dda-06ff4ba37edf.png" width="80%" /></p>

The **HTTP Request** component gets the data from url 
https://raw.githubusercontent.com/loko-ai/regression_from_web_dataset/master/data/diabetes.json, the **Function** component 
yields the rows of the dataset as a stream and finally the **Predictor** component fits the diabetes predictor.

Ones the model is fitted, you can open the Predictors tab and visualize the generated report:

<p align="center"><img src="https://github.com/Cecinamo/ner/assets/30443495/f444d90b-4336-4d20-97d2-f3a4f11528cf" width="80%" /></p>

### STEP2: Expose service

Finally, you can expose a service to obtain the diabetes predictions.

<p align="center"><img src="https://user-images.githubusercontent.com/30443495/231217493-dd0d6b70-e5fa-40c0-97a2-b6f79810ce1f.png" width="80%" /></p>

Use **Route** and **Response** components at the beginning and at the end of the flow producing the output. In the 
**Route** configuration name the service *predict* and copy the complete url (i.e. http://localhost:9999/routes/orchestrator/endpoints/regression_from_web_dataset/predict).
In the **Response** component set the *Response Type* to json. 

The **Function** component extracts the body from the received request and returns it to the **Predictor** component 
which predicts the output.

You can test it using:

```
curl -d '{"age": 0.0380759064, "sex": 0.0506801187, "bmi": 0.0616962065, "bp": 0.0218723855, "s1": -0.0442234984, "s2": -0.0348207628, "s3": -0.0434008457, "s4": -0.002592262, "s5": 0.0199074862, "s6": -0.0176461252}' -X POST http://localhost:9999/routes/orchestrator/endpoints/regression_from_web_dataset/predict
```

### STEP3: Test service

You can test the predict service directly in your flow using the **HTTP Request** component:

<p align="center"><img src="https://user-images.githubusercontent.com/30443495/231221294-f6a515c6-42d6-4f36-bb1a-78b1a1ce0faf.png" width="80%" /></p>

In this case you have change http://localhost:9999 to http://gateway:8080 since the request will be executed in one of 
the containers inside the loko network (i.e. http://gateway:8080/routes/orchestrator/endpoints/regression_from_web_dataset/predict).