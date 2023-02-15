# Political Party Classification using Sentiment Analysis

Name:       Devin Patel  
Class:      CS 588 - 01  
Term:       FA 22  
Project:    Using sentiment analysis and popularity stats
            on 2016 Presidential Election tweets to predict
            party affiliation based on sentiment analysis.  
<br>


# Data Collection

The data used was compiled by researchers Justin Littman, Laura Wrubel, and Daniel Kerchner. The dataset contains lists of twitter status IDs organized by party that relate to the 2016 Election. The data is hosted on the [Harvard Dataverse.](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/PDI7IN)  

The subset of data used for this project are the following:

| Data File                          |  Description  | Statuses Pulled |
| :---                               |  :---        |      -----:     |
| [democratic-candidate-timelines.txt](https://dataverse.harvard.edu/file.xhtml?persistentId=doi:10.7910/DVN/PDI7IN/KLFZRI&version=3.0) |  Status IDs of Democratic Candidate Hillary Clinton      |      20,000     |
| [democratic-party-timelines.txt](https://dataverse.harvard.edu/file.xhtml?persistentId=doi:10.7910/DVN/PDI7IN/TXWMVP&version=3.0)     |  Status IDs of Democratic Party Accounts      |      10,550     |
| [republican-candidate-timelines.txt](https://dataverse.harvard.edu/file.xhtml?persistentId=doi:10.7910/DVN/PDI7IN/PDQIEW&version=3.0) |  Status IDs of Republican Candidate Donald Trump      |      20,000     |
| [republican-party-timelines.txt](https://dataverse.harvard.edu/file.xhtml?persistentId=doi:10.7910/DVN/PDI7IN/A9OIZQ&version=3.0)     |  Status IDs of Republican Party Accounts      |      15,402     |

Each of these status IDs represent a specific twitter status (i.e., a tweet). These statuses and relevant data are pulled using the [Tweepy API](https://developer.twitter.com), after which sentiment analysis is performed on it using TextBlob.  

The following features will be extracted from each status as of November 23, 2022:  

|  Feature Name  |  Description                    |   DType | Range |
|  :-----------  |  :----------                    |   :--:  | :---:|
|  Likes         |  Number of Likes on a Status    |   int   | [0, &infin;) |
|  Retweets      |  Number of Retweets on a Status |   int   | [0, &infin;) |
|  Subjectivity  |  Sentiment value denoting how 'opinionated' the text is |  float       | [0, 1] |
|  Polarity      |  Sentiment value denoting positivity (1), neutrality (0), or negativity (-1) of the text | float | [-1, 1] |


The following classes are labeling the above data:  

|  Class #  |  Code  |  Name  |  Color (if applicable)  |
|  :-----:  |  :--:  |  :---  |  :--------------------  |
|  0        |  R     |  Republican  |  Red              |
|  1        |  D     |  Democrat    |  Blue             |

Once the data is compiled, it will be exported as a binary pickle file for quick imports and as a viewable file type CSV.  
<br>

# Data Processing

The data is then ran through various methods of dimensionality reduction and feature selection to determine which features to keep.  
- Principle Component Analysis (PCA)
- Linear Discriminant Analysis (LDA)
- Analysis of variance (ANOVA)

Afterwards, the following classifiers are tested against training subsets of various sizes.
- Gaussian Naive Bayes
- Support Vector Machine (RBF kernel)
- Multi-Level Perceptron Classifier

Finally, each classifier generates a confusion matrix using the best performing training subset size.  
<br>

# File Structure
The following file structure must be created in the working directory prior to running the program:
```
project
│   classifiers.ipynb
│   dimension_reduction.ipynb
│   preprocessing.ipynb
│
└───auth
│   │   config.json
│   
└───Data
│   │   democratic-candidate-timelines.txt
│   │   democratic-party-timelines.txt
│   │   republican-candidate-timelines.txt
│   │   republican-party-timelines.txt
│
└───Figures
│   │
│   └───classifiers
│   │   │
│   │   └───Confusion
│   │
│   └───dimension_reduction
│
└───Logs
```

`config.json` must be configured with the proper [Tweepy API](https://developer.twitter.com) credentials in the `auth` directory according to the following:  
```json
{
    "KEY": "API Key goes here",
    "SECRET": "API Secret goes here",
    "BEARERTOKEN": "Bearer Token goes here",
    "TOKEN": "Access Token goes here",
    "TOKENSECRET": "Access Token Secret goes here"
}
```

<br>

# Dependencies
All packages installed using `pip v22.3.1`.

|  Tool/Library  |  Version  |  Purpose  |
|  :----------:  |  :------  |  :------  |
|  python        |  3.10.8   |  Programming Language |
|  jupyter       |  1.0.0    |  Notebook for Python  |
|  ipykernel     |  6.17.1   |  Running Jupyter Notebook |
|  numpy         |  1.23.5   |  Organizing Data  |
|  pandas        |  1.5.1    |  Organizing Data  |
|  scikit-learn  |  1.1.3    |  Data Analysis Methods  |
|  matplotlib    |  3.6.2    |  Plotting Data  |
|  seaborn       |  0.12.1   |  Plotting Heatmaps  |
|  dataframe_image  |  0.1.3 |  Exporting pandas.DataFrame as png  |
|  textblob      |  0.17.1   |  Sentiment analysis  |
|  tweepy        |  4.12.1   |  Access to Twitter database  |

**Note** that `textblob` must also run `python3 -m textblob.download_corpora` to complete installation of `textblob`.
