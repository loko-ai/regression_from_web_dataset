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

You can then go back to the project and fit the diabetes model:

