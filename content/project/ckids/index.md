---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Tracking Health and Nutrition Signals from Social Media Data"
summary: ""
authors: []
tags: ['NLP', 'Social Media', 'Web Scraping', 'Data Analysis', 'Modeling']
categories: []
date: 2020-03-28T10:42:05-08:00

# Optional external URL for project (replaces project detail page).
external_link: ""

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: "Smart"
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---
<!-- 
![](https://github.com/EricaXia/shelter/raw/master/imgs/rescue-animals-and-shelter-pups.jpg) -->
### Instgram Web Scraping and Data Analysis Project
#### Center for Knowledge-Powered Interdisciplinary Data Science (CKIDS) at USC
Project Advisors:  
<br />
Professor Andrés Abeliuk, Information Sciences Institute, USC  
<br />
Dr. Abigail Horn, Postdoctoral Fellow, Preventive Medicine, USC


---

**Description:** 
Social media provides an abundance of data for diet and nutritional behaviors. We are interested in whether social media data from Instagram serves as a reliable indicator into nutrition and dietary health despite implicit biases (self-presentation and self-selection).


---

#### Table of Contents

1. [Background and Motivation](#1-background)
2. [Visualization](#2-visualizations)
3. [Modeling & Analysis](#3-modeling-and-analysis)
4. [Web App Deployment to Heroku](#4-web-app-deployment)
---

## 1. Background 

<br />

Official public health estimates population-level nutritional quality and patterns come from self-report survey data based on small samples and provide coarse surveillance measures; the best available data source in Los Angeles employs a sample population on the order of 5,000 LA residents to provide a limited set of diet/nutrition variables such as frequency of fruit and vegetable consumption and fast food consumption. Social media data suffers from multiple important biases including self-presentation and self-selection, but provides information that survey data cannot: it is at a large population scale, can provide sentiment information, and demonstrate social components including likes, follows, and behavior clustering. Using an Instagram dataset of all geo-located posts at food outlets in Los Angeles for 3 months in 2014, this project will investigate whether Instagram posts, despite implicit biases (and to the extent possible, accounting for these biases), can provide a representative health signal, informative of the quality of population nutrition and dietary patterns at a highly-resolved (e.g. census tract level) spatial scale. 

<br />

There is an ongoing discourse in public health fields regarding the validity of social media data for diet and nutritional behavior surveillance, and how it compares to official measures, and/or what we can learn from this data that has practical health significance, but to date these research questions have not been investigated directly (largely out of a general disbelief of its utility). Therefore regardless of whether this project finds strong or weak indications, the work will contribute to the ongoing conversation on whether or not social media data can provide a signal into nutrition and dietary health. 

## 2. Visualizations

After cleaning, we can run some basic Exploratory Data Analysis to investigate and better understand our data. 

- What's the count of animals being adopted or not?

![](https://github.com/EricaXia/shelter/raw/master/imgs/eda0.PNG)

From the normalized value counts of the dataset, we have about 60/40 ratio of animals being adopted/euthanized.

- What's the distribution of animal age by outcome type?

![](https://github.com/EricaXia/shelter/raw/master/imgs/eda3.PNG)

On average, euthanized animals have higher average ages. Adopted animals tend to be at younger ages. The distributions both still seem to be right skewed, since most animals won't live as long as twenty years old, and most animals who come into the shelter are of younger age.

- What's the count of animals by type (cat or dog) being adopted?

![](https://github.com/EricaXia/shelter/raw/master/imgs/eda4.PNG)

There's a slightly greater number of cats than dogs overall at the shelter. Thus, more cats get adopted and euthanized compared to dogs. Both cats and dogs get adopted at about the same ratio to total cats and dogs (70% adoption rate).

<br />
## 3. Modeling and Analysis

### 3.1. One Hot Encoding (Categorical) and Standardizing (Numerical)
To train a classifier model, we need to convert all categorical features to numerical so the model can interpret them. Additionally, we'll scale the numerical feature "Age" by standardization.  These tasks are done with the OneHotEncoder and StandardScaler from the scikit-learn library.

### 3.2. Modeling
Once all the features are converted to appropriate formats that the model can interpret, it's time to build the model. In sklearn, a pipeline is defined to transform, split, and model the data. We use a Logistic Regression model with the LBFGS solver. 

```
categorical_transformer = Pipeline(steps = [('onehot', OneHotEncoder(handle_unknown='ignore'))])

preprocessor = ColumnTransformer(
    transformers=[
        ('num', numeric_transformer, numeric_features),
        ('cat', categorical_transformer, categorical_features)])
        
# Append classifier to preprocessing pipeline
clf = Pipeline(steps=[('preprocessor', preprocessor),
                      ('classifier', LogisticRegression(solver='lbfgs', max_iter = 500))])

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

clf.fit(X_train, y_train)
y_pred = clf.predict(X_test)
print("model score: %.3f" % clf.score(X_test, y_test))

# gets the predicted probabilities
prob = clf.predict_proba(X_test)[:,1]

```

As a final visual, we can view the coefficients most positively and negatively correlated with adoption chance.

![](https://github.com/EricaXia/shelter/raw/master/imgs/eda_last.PNG)

The features most strongly impacting adoption chances are animal health. Healthy animals are likely to be adopted, while untreatable animals are very unlikely to be adopted, likely due to low survival rate.

### 3.3. Error Analysis

The ROC and Precision-Recall curves can give us some insight into the model performance. The ROC curve shows the true positive rate and false positive rate (sensitivity and specificity) tradeoff for the logistic regression model. Given the area under the curve (which measures ability to correctly predict class) is 0.86, the model displays some skill in predicting outcomes.

![](https://github.com/EricaXia/shelter/raw/master/imgs/LogReg_ROC.png)

The PRC shows the tradeoff between precision (positive predictive value) and recall (sensitivity) at different classification thresholds (classifying an observation as adopted if probability is above a certain value we vary). Since PRCs tend to be more constant and thus more reliable for imbalanced datasets such as ours, we prefer to use this curve for our analysis. The closer the curve is to the upper right corner, the better the prediction is. (A perfect test would have a curve overlapping the upper right corner with both prec/recall equal to 1.)

![](https://github.com/EricaXia/shelter/raw/master/imgs/pr_curve.png)


## 4. Web App Deployment

The model is contained within a Python script. A web application can create interactivity with users by collecting their input and providing a prediction output. We can build a web application using Flask, a "microframework" for building smaller apps. To collect the data from users, we design an HTML template for users to interact with the web application, with different options (such as animal type, age, and color) to feed into the model.

<center>
{{< figure library="true" src="htmlform.png" title="Static HTML Form" lightbox="true" >}}
</center>


After creating the static page, we use Flask to host it. First, a conda virtual environment is created to contain all dependencies. Then, we create a Python file called 'script.py' used to run Flask and the model. In the code below, the ValuePredictor function takes in the user's input from the form, converts the input to the correct format, and feeds it to the model (stored in a .pkl file). The function returns the final prediction and predicted probability.

```
def ValuePredictor(to_predict_list):
    to_predict_dict = {k: v for k, v in zip(cols, to_predict_list)}
    to_predict = pd.DataFrame(data=to_predict_dict, columns=cols, index=[0])
    loaded_model = pickle.load(open("clf_model.pkl","rb"))
    result = loaded_model.predict(to_predict)
    prob = loaded_model.predict_proba(to_predict)[:,0]
    return(result[0], prob[0])


@app.route('/result',methods = ['POST'])
def result():
    if request.method == 'POST':
        to_predict_list = request.form.to_dict()
        to_predict_list=list(to_predict_list.values())
        outcome = ValuePredictor(to_predict_list)
        
        if outcome[0]== "ADOPTION":
            prediction = 'ADOPTION'
            probability = '{:.2%}'.format(np.round(outcome[1], decimals=2))
            
            
        elif outcome[0] == "EUTHANIZE":
            prediction='EUTHANIZE'
            probability = '{:.2%}'.format(np.round(outcome[1], decimals=2))
            
        return render_template("result.html", prediction = prediction, probability = probability)

```

A separate HTML file displaying the prediction and probability is created to show the user's results. To host the app online, we deploy the app to Heroku, a free plaform that lets us run apps online in the cloud. 

{{< figure library="true" src="heroku.png" lightbox="true" >}}