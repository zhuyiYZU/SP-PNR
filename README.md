# SP-PNR
A fine-tuned approach to news recommendation
README

Dataset Download Instructions
We have uploaded the dataset to Baidu Netdisk, making it available for researchers to download and use. Below are the link and access code details:
Download Link: https://pan.baidu.com/s/1Og_e-KQpc_3C5ay77fp_AQ

Access Code: 7skm

If you encounter any issues during the download or usage process, feel free to contact us via email:
Email: yuanxuyzu@163.com

Dataset Usage
After downloading, please extract the dataset to the following directory under the project root:

bash

    datasets/
    └── mind/
        └── (extracted data files)

Make sure the dataset path is correctly set before running the project code.

Model Download Instructions
This project uses the bert-base-cased model, which needs to be downloaded from the Hugging Face website. Please follow the steps below:

Visit the Hugging Face model page: https://huggingface.co/google-bert/bert-base-cased

Download the model files and place them in the following directory under the project root:

bash

    model/
    └── bert-base-cased
Make sure the model path is correctly set in your code before running the project.


Environment Setup

The required dependencies for this project are listed in the requirements.txt file. You can install all necessary packages using the following command:

bash

pip install -r requirements.txt

Recommendation: It is advised to use a virtual environment (e.g., venv or conda) to isolate the project environment and avoid conflicts with other projects.

Extension for Data Loading
We have added support for loading the MIND dataset in the text_classification_dataset module under the openprompt directory. Below is the updated code for the data loader:

Example Code
python


    class MINDProcessor(DataProcessor):
        def __init__(self):
            super().__init__()
            self.labels = ["dislike", "like"]
    
        def get_examples(self, data_dir, split):
            path = os.path.join(data_dir, "{}.tsv".format(split))
            examples = []
            with open(path, encoding='utf8') as f:
                reader = csv.reader(f, delimiter='\t')
                for idx, row in enumerate(reader):
                    label, new_title, sub, sum = row
                    text_a = new_title.replace('\\', ' ')
                    text_b = sub.replace('\\', ' ')
                    text_c = sum.replace('\\', ' ')
                    example = InputExample(
                        guid=str(idx), 
                        label=int(label), 
                        text_a=text_a, 
                        text_b=text_b, 
                        text_c=text_c
                    )
                    examples.append(example)
            return examples

Usage
Add the MINDProcessor class to your module where processors are defined.


Once the setup is complete, you can execute the run.py script to start the experiment:

bash

    python run.py
Upon completion, the results will be automatically saved to the result directory under the project root. You can analyze the output as per your requirements.

