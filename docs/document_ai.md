# <h1black>Document </h1black><h1blue>AI</h1blue>
## <h1grey>Build and Run Two Document AI models</h1grey>

In this section you will learn how to build and train a Document AI Model which will enable you to extract important structured content out of unstructured documents.

- Within the AI & ML area, click on **Document AI**:

    ![alt text](assets/docai/D001.png)

- Click on the + Build icon to build a new model

    ![alt text](assets/docai/D002.png)

- Under Build name, type in **ANALYST_REPORTS**

- Choose the **DATAOPS_EVENT_PROD** for the database and **DOCUMENT_AI** for the Schema

![create build](assets/docai/D003.png)

Press **Create**

### <h1sub>Downloading Documents</h1sub>

We now need upload some documents into Document AI in order to build a train model.  The first Model we will build are analyst reports.  The reports we we will be using are completely fictional.

- **Download** The Analyst Reports **<a href="downloads/research_analyst_reports.zip" download>here</a>**



### <h1>Uploading the Documents to the model</h1>
- Unzip the Analyst reports to a file location which you can access
- Open the model which you have just created and press upload documents

![upload_docs](assets/docai/D004.png)

You will see that you can upload a variety of formats.  Today we will be uploading PDF documents.  You can either select the files by searching in your file system **or** drag and drop.

![upload_docs](assets/docai/D005.png)


Press **Upload**

You will see that 6 documents are now uploaded but need attention.  To use the model, you will first need to decide which fields you would like to extract.  A warning will also let you know that for better accuracy you should really train the model with more documents.  For this exercise we will just use 6 but in reality you will need to train the model with at least 10 documents for good accuracy.

### <h1sub>Review Documents and Extract Fields</h1sub>

- With in the Documents in Dataset section, press **See all documents**

You willl see that all 6 documents are in need of review

- Click on the first document in the list.  This will take you straight to the Analyst Report.  The right hand side of the screen you will need to add the fields that you wish to extract.  We will be extracting specific fields.

- Press **+ Value** to add a new field

- Enter **DATE_REPORT** in the first field and in the second field, as the question **When was the Report Created?**

Document AI will search through the multi page document and then will give you an answer with a probability score

![upload_docs](assets/docai/D006.png)

- If you are happy with the answer, mark it with the **tick**.  When the press the tick, the probability score will change to 1.00 - In otherwords, you have told document AI that you are 100% sure that this answer is correct.

- Create 5 additional fields with the corresponding questions - If document AI get's the answer right, mark with a tick. press **+ Value** to create each field.

| Field    | Question |
| -------- | -------  |
| NAME_OF_REPORT_PROVIDER | name of the report provider   |
| RATING | What is the rating? is it BUY, SELL, HOLD OR EQUAL-WEIGHT?     |
| CLOSE_PRICE    | Close Price Value    |
| PRICE_TARGET    | Price Target Value    |
| GROWTH   | What is the latest revenue Growth - YoY    |

If the answer is wrong, overtype the answer with the correct answer.  This will automatically mark it as correct with the new answer.

Sometimes document AI comes up with no answer at all.  If this is correct, still mark with a tick.

When you have finished entering the questions and getting the answers you should see something that looks like this:

![upload_docs](assets/docai/D007.png)

Now it's time to evaluate the same questions and answers with another document.

- Click on the arrow to review on the bottom right of this pane the next document.  Currently you are reviewing 1 of 6 documents.

The next document may populate more of the answers.  You will need to simply mark them as to whether they are correct or not.  If any are incorrect, type over with the correct answer.

- When you have finished reviewing 2 of 6 documents, continue to review the final 5 documents. 


Once you have completed your document review press the back button on the top left to go back to the previous screen

![upload_docs](assets/docai/D008.png)

All 6 documents should now be marked as **Accepted**. 

- Go back to Build Details

You will see that there is a model accuracy.  This accuracy figure will be due to how many answers document ai initially predicted correctly or not.  If the accuracy score is low, you may wish to train the model by clicking on **Train model** button. This will retrain the model using the corrected answers.

- Press **Publish Version**  which will publish your first version of the model.  Today, we will not **train model** as this can take some time - especially if you are training large documents of multiple pages.  In addition, the model is calculating a high model accuracy score of 0.95.  Being concise with your questions can help the accuracy with little need for training.

Once complete, you will see a model version number and example queries on how to utilise the model in **SQL**

![create build](assets/docai/D009.png)

You will have examples of these queries preloaded into a notebook. This model is iterative, if you find the results are not what you expect in terms of accuracy, simply add more documents and retrain.  The more documents you train, the better results you will get.  Every time you re-train or republish a new version, you will get a new version number.  You will need this version number in the query.  The screenshot above, shows that you are using the **model version 1**.

- Press the **back button** to return to the Document AI home screen.


### <h1sub>Create a second model</h1sub>


The Second model we will build are consistant infographic style reports.  These are quartely publically available snowflake reports.

- **Download** the Infographics **<a href="downloads/infographics.zip" download> here</a>**

You will now create a new model - this time, we will call it **INFOGRAPHICS**

- Go back to the document AI home page and click on the **+ build** button to build a new model and populate the fields with the following:

Build name: **INFOGRAPHICS**
Location: 

- Database **DATAOPS_EVENT_PROD** 
- Schema **DOCUMENT_AI**

Press **Create**

Upload the previously downloaded **Infographic** files using the Upload documents button.

- Train the model with the following fields

| Field    | Question |
| -------- | -------  |
| PROD_REVENUE | What is the product revenue (choose Q if it specifies)  |
| NET_REVENUE_RETENTION | What is the net revenue retention rate     |
| TOTAL_CUSTOMERS    | TOTAL CUSTOMERS    |
| TOTAL_M_CUSTOMERS   | Number of $1 + Customers    |
| GLOBAL_2000_CUSTOMERS   | How many forbes global 2000 customers are there?    |
| MARKETPLACE_LISTINGS  | how many marketplace listings are there?    |
| DATE_OF_REPORT   | What is the date of the report    |
| QUARTER   | What is the quarter of the report Q1, Q2, Q3 or Q4    |

- Add all the fields the same way as previously
- Remember to evaluate each field by pressing the tick when correct, or correcting manually if incorrect
- Remember to review ALL documents

You should finish with answers similar to this.  Remember to correct answers which are incorrect.

![create build](assets/docai/D010.png)



- Press **Publish Version** to publish a new version.  Do not press train as this may take too much time for the lab.  The accuracy score is also very high as the model has given the correct answers without training.

You will now have a second model which will allow you to extract the infographic information into a structured table.

You have now created two models to process documents.  

### <h1sub>Process Documents at Scale</h1sub>

Let's now process some documents.  We have more documents both for Analyst Reports and infographics in a stage.  We can use our new models to extract structured information out of them.  In addition, we will extract all the text out of the Analyst reports for search purposes.

For the next Document AI steps, you will use **Snowflake Notebooks** to process the documents as well as **visualise** the outputs.

#### <h1sub>Model 1 - Analyst Reports</h1sub>
- Go back to the home page and click on **Projects > Notebooks**

![notebooks](assets/projects_notebooks2.png)
- Click on the **Document AI Analyst Reports** notebook

- Run through the notebook to process the **Analyst Reports**.

This notebook will perform the following:

-   Extract the values defined in the **ANALYST_REPORTS** model you have created from a directory of files residing in a **Snowflake Stage**

-   Create a structured table of information

-   Extract all remaining text using **Cortex Parse Document**

#### <h1sub>Model 2 - Infographics</h1sub>

You will run a second notebook which will also extract the structured text out of the **Infographic** image files stored in a **Snowflake Stage**.

- Go back to the Notebooks and open the **INFOGRAPHICS** notebook

![notebook](assets/go_to_notebooks.png)

- Run through the notebook to process the **Infographics** which will extract all values and store the results in a new structured table.

