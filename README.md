## League of Legends Ability Generation
Done in Python using PyCharm
This project uses Generative Pre-trained Transformer 2 [(GPT-2)](https://en.wikipedia.org/wiki/GPT-2) to generate new text after being trained with pre-existing datasets.

Only datasets used and samples for each will be provided here, as models take up too much space.
Refer to [here](https://github.com/openai/gpt-2/blob/master/DEVELOPERS.md) in order to install required libraries.

117M parameter model was used, but there are multiple with more available.

Datasets can contain any data, as long as it is in English. You CAN train in other languages, but it might take much more time before the same precision/accuracy is reached, if at all. I used League of Legends ability descriptions, manually copied and modified from [here](https://leagueoflegends.fandom.com/wiki/List_of_champions).

In any of the 3 datasets here chunks of text are delimited using `<|endoftext|>`, in order for the model to learn the formatting of abilities.

Assuming you're in the terminal in the main folder (there should be a src folder within, and no other) and that you have installed the appropriate model.
Firstly copy train.py and encode.py into the src folder.
Move the current folder into src.
You need to encode the dataset. Use the following code:

    python encode.py path_to_dataset.txt name_of_encoded_file.npz
Additional arguments exist, but they aren't necessary. Check them out within the encode.py file.
Issues might occur regarding the model name and path to the model. Search within the file for these and change them if necessary.

After encoding, you may now train using that file. Use the following code:

    python train.py --dataset name_of_encoded_file.npz
You can also add the following optional arguments:

    --run_name run_folder_name
    --batch_size 2
    --learning_rate 0.0001
Batch size and learning rate should only be changed should the model fail to lower its losses.
You can cancel the training at any time using Ctrl + C. You can also continue training by just repeating the initial training code, as long as you add the right run name.

You can generate samples using trained models with the following code:

    python generate_unconditional_samples.py --model_name model_name
This generates samples until interrupted using Ctrl + C.
Also available is interactive generation, where you enter some text manually, then the model attempts to finish it. Use the following code:

    python interactive_conditional_samples.py --model_name lyric
For both sample generations you can add these optional arguments:

    --temperature 0.8
    --top_k 40
Lower temperature makes the model output words with lower probability more often. Default is 1.
Changing top_k affects how many words are considered at a time when outputing. Default is 0.

