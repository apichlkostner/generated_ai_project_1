# Project 1 of course "Generative AI" from Udacity

Lightweight fine-tuning of a LLM

## Dataset

HuggingFace dataset "dair-ai/emotion"

This dataset contains sentences with a classification of emotion.

### Labels

| Label    | Number |
|----------|--------|
| sadness  | 0      |
| joy      | 1      |
| love     | 2      |
| anger    | 3      |
| fear     | 4      |
| surprise | 5      |

### Examples

| Sentence                                                                                                      | Emotion   |
|---------------------------------------------------------------------------------------------------------------|-----------|
| i hate not feeling useful                                                                                     | joy       |
| i reflect back on all the beer i drank i feel shamed                                                          | sadness   |
| i had begun to feel apprehensive when thick black rain clouds stormed into the sky above town                 | fear      |
| i do now as compared with years ago is that i no longer feel i have to be accepted by others only those who matter to me | love      |
| i feel like each kid left school this year with at least three pieces they were really proud of               | sadness   |
| i actually feel solidarity with the americans who went on to cry for blood in iraq tortured prisoners and the stripping of the bill of rights | fear      |
| i feel that when i run i that is me sarah the mind am supporting this body                                    | sadness   |
| i feel suspicious when i see this redundant use of the credential                                             | fear      |
| i do feel lonely at times and at times i still feel that i am alone                                           | sadness   |
| i miss the feeling of loving                                                                                  | love      |

## Preparation

- The dataset is loaded.
- The GPT2 model with classification head is loaded.
- The GPT2 tokenizer is loaded and an padding token is added. The model is updated with the new token
- Tokens are added to the dataset with the tokenizer

## Training of the GPT2 with classification head

- A HugginFace trainer is set up and the model is trained
- The trained model is evaluated with an accuracy of 0.58

## Adding LoRA

- A LoRA layer is added
- The new model is optimized with a trainer
- The model is evaluated with an accuracy of 0.93

## Test with QLoRA

- Additional to LoRA the base model is used with a lower quantization
- The model is evaluated with an accuracy of 0.93, no difference to the model with full quantization
- It needed less GPU memory

## Test with different hyperparameter

Test with different hyperparameter "learning rate", "dropout" and LoRA parameter "r", "weight decay" had mostly similar accuracy. Only a too high learning rate gave a low accuracy of 0.3.

## Result

Using LoRA for fine-tuning the GPT2 gave a much better result than just adding a classification head to a pretrained GPT2. The accuracy on the test set is increased from 0.54 to 0.93.

Different hyperparameter mostly didn't change too much on the result, so the initial parameters were already a good choice. Too small learning rate gave a lower accuracy but with more epochs it should give also good results.

With QLoRA the memory consumption could be decreased so even larger models can be trained with the limited GPU memory resource. In this case, the result was comparable with the model with full quantization.

