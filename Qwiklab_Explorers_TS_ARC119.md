# Create a Secure Data Lake on Cloud Storage: Challenge Lab || [GSP119](https://www.cloudskillsboost.google/course_templates/704/labs/461627) ||

# # Like, comment, share & Don't forget to subscribe [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN) 👍😄🤝

### Run the following Commands in CloudShell

```bash
export ZONE=
```

```bash
export KEY_1=domain_type

export VALUE_1=source_data

```

```bash
export REGION="${ZONE%-*}"

#TASK 1
gsutil mb -p $DEVSHELL_PROJECT_ID -l $REGION -b on gs://$DEVSHELL_PROJECT_ID-bucket/


#TASK 2
gcloud alpha dataplex lakes create customer-lake \
--display-name="Customer-Lake" \
 --location=$REGION \
 --labels="key_1=$KEY_1,value_1=$VALUE_1"


gcloud dataplex zones create public-zone \
    --lake=customer-lake \
    --location=$REGION \
    --type=RAW \
    --resource-location-type=SINGLE_REGION \
    --display-name="Public-Zone"


gcloud dataplex environments create dataplex-lake-env \
           --project=$DEVSHELL_PROJECT_ID --location=$REGION --lake=customer-lake \
           --os-image-version=1.0 --compute-node-count 3  --compute-max-node-count 3 


#TASK3

gcloud dataplex assets create customer-raw-data --location=$REGION \
            --lake=customer-lake --zone=public-zone \
            --resource-type=STORAGE_BUCKET \
            --resource-name=projects/$DEVSHELL_PROJECT_ID/buckets/$DEVSHELL_PROJECT_ID-customer-bucket \
            --discovery-enabled \
            --display-name="Customer Raw Data"


gcloud dataplex assets create customer-reference-data --location=$REGION \
            --lake=customer-lake --zone=public-zone \
            --resource-type=BIGQUERY_DATASET \
            --resource-name=projects/$DEVSHELL_PROJECT_ID/datasets/customer_reference_data \
            --display-name="Customer Reference Data"

#TASK 4


# gcloud data-catalog tag-templates create customer_data_tag_template \
#    --project=$DEVSHELL_PROJECT_ID \
#    --location=$REGION \
#    --display-name="Customer Data Tag Template"
#    --field=id=DataOwner,display-name=Data\ Owner,type=string,required=TRUE \
#    --field=id=PIIData,display-name=PII\ Data,type='enum(Yes|No)',required=TRUE

# gcloud data-catalog tag-templates create customer_data_tag_template \
#     --project=$DEVSHELL_PROJECT_ID \
#     --location=$REGION \
#     --display-name="Customer Data Tag Template" \
#     --field=id=DataOwner,type=string,display-name="Data Owner" \
#     --field=id=PIIData,type='enum(Yes|No)',display-name="PII Data"
```

# Congratulations ..!!🎉  You completed the lab shortly..😃💯

# *Well done..!* 👏

# Thank you for visiting.... :) 🗯️

# [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN)
