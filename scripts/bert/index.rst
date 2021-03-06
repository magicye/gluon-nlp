Bidirectional Encoder Representations from Transformers
-------------------------------------------------------

:download:`[Download] </model_zoo/bert.zip>`

Reference: Devlin, Jacob, et al. "`Bert: Pre-training of deep bidirectional transformers for language understanding. <https://arxiv.org/abs/1810.04805>`_" arXiv preprint arXiv:1810.04805 (2018).

The following pre-trained BERT models are available from the **gluonnlp.model.get_model** API:

+-----------------------------+----------------+-----------------+
|                             | bert_12_768_12 | bert_24_1024_16 |
+=============================+================+=================+
| book_corpus_wiki_en_uncased | ✓              | ✓               |
+-----------------------------+----------------+-----------------+
| book_corpus_wiki_en_cased   | ✓              | ✓               |
+-----------------------------+----------------+-----------------+
| wiki_multilingual_uncased   | ✓              | x               |
+-----------------------------+----------------+-----------------+
| wiki_multilingual_cased     | ✓              | x               |
+-----------------------------+----------------+-----------------+
| wiki_cn_cased               | ✓              | x               |
+-----------------------------+----------------+-----------------+

where **bert_12_768_12** refers to the BERT BASE model, and **bert_24_1024_16** refers to the BERT LARGE model.

BERT for Sentence Classification on GLUE tasks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

GluonNLP provides the following example script to fine-tune sentence classification with pre-trained
BERT model.

+---------------------+--------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+
|                     |                                                  MRPC                                                  |                                                  RTE                                                  |                                                 SST-2                                                 |                                                MNLI-m/mm                                               |
+---------------------+--------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+
|        model        |                                             bert_12_768_12                                             |                                             bert_12_768_12                                            |                                             bert_12_768_12                                            |                                             bert_12_768_12                                             |
+---------------------+--------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+
| validation accuracy |                                                  88.7%                                                 |                                                 70.8%                                                 |                                                  93%                                                  |                                             84.55%, 84.66%                                             |
+---------------------+--------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+
|      batch_size     |                                                   32                                                   |                                                   32                                                  |                                                   16                                                  |                                                   32                                                   |
+---------------------+--------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+
|        epochs       |                                                    3                                                   |                                                   3                                                   |                                                   4                                                   |                                                    3                                                   |
|                     |                                                                                                        |                                                                                                       |                                                                                                       |                                                                                                        |
+---------------------+--------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+
|       epsilon       |                                                  1e-6                                                  |                                                  1e-6                                                 |                                                  1e-6                                                 |                                                  1e-8                                                  |
+---------------------+--------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+
|     training log    | `log <https://raw.githubusercontent.com/dmlc/web-data/master/gluonnlp/logs/bert/finetuned_mrpc.log>`__ | `log <https://raw.githubusercontent.com/dmlc/web-data/master/gluonnlp/logs/bert/finetuned_rte.log>`__ | `log <https://raw.githubusercontent.com/dmlc/web-data/master/gluonnlp/logs/bert/finetuned_sst.log>`__ | `log <https://raw.githubusercontent.com/dmlc/web-data/master/gluonnlp/logs/bert/finetuned_mnli.log>`__ |
+---------------------+--------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+
|       command       |                                                   [1]                                                  |                                                  [2]                                                  |                                                  [3]                                                  |                                                   [4]                                                  |
+---------------------+--------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+

For all model settings above, we set learing rate = 2e-5 and optimizer = bertadam.

[1] MRPC

.. code-block:: console

    $ curl -L https://tinyurl.com/yaznh3os -o download_glue_data.py
    $ python3 download_glue_data.py --data_dir glue_data --tasks MRPC
    $ GLUE_DIR=glue_data finetune_classifier.py --task_name MRPC --batch_size 32 --optimizer bertadam --epochs 3 --gpu --lr 2e-5

[2] SST-2

.. code-block:: console

    $ curl -L https://tinyurl.com/yaznh3os -o download_glue_data.py
    $ python3 download_glue_data.py --data_dir glue_data --tasks SST
    $ GLUE_DIR=glue_data python3 finetune_classifier.py --task_name SST --epochs 4 --batch_size 16 --optimizer bertadam --gpu --lr 2e-5 --log_interval 500

[3] RTE

.. code-block:: console

    $ curl -L https://tinyurl.com/yaznh3os -o download_glue_data.py
    $ python3 download_glue_data.py --data_dir glue_data --tasks RTE
    $ GLUE_DIR=glue_data python3 finetune_classifier.py --task_name RTE --batch_size 32 --optimizer bertadam --epochs 3 --gpu  --lr 2e-5

[4] MNLI

.. code-block:: console

    $ curl -L https://tinyurl.com/yaznh3os -o download_glue_data.py
    $ python3 download_glue_data.py --data_dir glue_data --tasks MNLI
    $ GLUE_DIR=glue_data python3 finetune_classifier.py --task_name MNLI --max_len 80 --log_interval 100 --epsilon 1e-8 --gpu

Some other tasks can be modeled with `--task_name` parameter.

BERT for Question Answering on SQuAD
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------------+---------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
|                       |                                                            SQuAD 1.1                                                            |                                                             SQuAD 1.1                                                            |                                                             SQuAD 2.0                                                            |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
|         model         |                                                          bert_12_768_12                                                         |                                                          bert_24_1024_16                                                         |                                                          bert_24_1024_16                                                         |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
|           F1          |                                                              88.53                                                              |                                                               90.97                                                              |                                                               77.96                                                              |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
|           EM          |                                                              80.98                                                              |                                                               84.05                                                              | 81.02                                                                                                                            |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
|       batch_size      |                                                                12                                                               |                                                                 4                                                                |                                                                 4                                                                |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
| gradient accumulation |                                                               None                                                              |                                                                 6                                                                |                                                                 8                                                                |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
|         epochs        |                                                                2                                                                |                                                                 2                                                                |                                                                 2                                                                |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
|      training log     | `log <https://raw.githubusercontent.com/dmlc/web-data/master/gluonnlp/logs/bert/finetune_squad1.1_base_mx1.5.0b20190216.log>`__ | `log <https://raw.githubusercontent.com/dmlc/web-data/master/gluonnlp/logs/bert/finetune_squad1.1_large_mx1.5.0b20190216.log>`__ | `log <https://raw.githubusercontent.com/dmlc/web-data/master/gluonnlp/logs/bert/finetune_squad2.0_large_mx1.5.0b20160216.log>`__ |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
|        command        |                                                               [5]                                                               |                                                                [6]                                                               |                                                                [7]                                                               |
+-----------------------+---------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+

For all model settings above, we set learing rate = 3e-5 and optimizer = adam.

BERT BASE on SQuAD 1.1
++++++++++++++++++++++

[5] bert_12_768_12

.. code-block:: console

    $ python finetune_squad.py --optimizer adam --batch_size 12 --lr 3e-5 --epochs 2 --gpu
 
Note that this requires about 12G of GPU memory. If your GPU memory is less than 12G, you can use the following command to achieve a similar effect. This will require approximately no more than 8G of GPU memory. If your GPU memory is too small, please adjust *accumulate* and *batch_size* arguments accordingly.

.. code-block:: console

    $ python finetune_squad.py --optimizer adam --accumulate 2 --batch_size 6 --lr 3e-5 --epochs 2 --gpu


BERT LARGE on SQuAD 1.1
+++++++++++++++++++++++

[6] bert_24_1024_16

.. code-block:: console

    $ python finetune_squad.py --bert_model bert_24_1024_16 --optimizer adam --accumulate 6 --batch_size 4 --lr 3e-5 --epochs 2 --gpu
    
Note that this requires about 14G of GPU memory.


BERT LARGE on SQuAD 2.0
+++++++++++++++++++++++

For SQuAD 2.0, you need to specify the parameter *version_2* and specify the parameter *null_score_diff_threshold*. Typical values are between -1.0 and -5.0. Use the following command to fine-tune the BERT large model on SQuAD 2.0 and generate predictions.json, nbest_predictions.json, and null_odds.json.

[7] bert_24_1024_16

.. code-block:: console

    $ python finetune_squad.py --bert_model bert_24_1024_16 --optimizer adam --accumulate 8 --batch_size 4 --lr 3e-5 --epochs 2 --gpu --null_score_diff_threshold -2.0 --version_2

To get the score of the dev data, you need to download the dev dataset (`dev-v2.0.json <https://rajpurkar.github.io/SQuAD-explorer/dataset/dev-v2.0.json>`_) and the evaluate script (`evaluate-2.0.py <https://worksheets.codalab.org/rest/bundles/0x6b567e1cf2e041ec80d7098f031c5c9e/contents/blob/>`_). Then use the following command to get the score of the dev dataset.

.. code-block:: console

    $ python evaluate-v2.0.py dev-v2.0.json predictions.json

.. code-block:: json
    
    {
        "exact": 77.958392992504,
        "f1": 81.02012658815627,
        "total": 11873,
        "HasAns_exact": 73.3974358974359,
        "HasAns_f1": 79.52968336389662,
        "HasAns_total": 5928,
        "NoAns_exact": 82.50630782169891,
        "NoAns_f1": 82.50630782169891,
        "NoAns_total": 5945
    }

BERT for Sentence or Tokens Embedding
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The goal of this BERT Embedding is to obtain the sentence and token embedding from BERT's pre-trained model. In this way, instead of building and do fine-tuning for an end-to-end NLP model, you can build your model by just utilizing the sentence or token embeddings.

Usage
+++++

.. code-block:: python

    from bert.embedding import BertEmbedding

    bert_abstract = """We introduce a new language representation model called BERT, which stands for Bidirectional Encoder Representations from Transformers.
     Unlike recent language representation models, BERT is designed to pre-train deep bidirectional representations by jointly conditioning on both left and right context in all layers.
     As a result, the pre-trained BERT representations can be fine-tuned with just one additional output layer to create state-of-the-art models for a wide range of tasks, such as question answering and language inference, without substantial task-specific architecture modifications.
    BERT is conceptually simple and empirically powerful.
    It obtains new state-of-the-art results on eleven natural language processing tasks, including pushing the GLUE benchmark to 80.4% (7.6% absolute improvement), MultiNLI accuracy to 86.7 (5.6% absolute improvement) and the SQuAD v1.1 question answering Test F1 to 93.2 (1.5% absolute improvement), outperforming human performance by 2.0%."""
    sentences = bert_abstract.split('\n')
    bert_embedding = BertEmbedding()
    result = bert.embedding(sentences)

If you want to use GPU, please import mxnet and set context

.. code-block:: python

    import mxnet as mx
    from bert.embedding import BertEmbedding

    ctx = mx.gpu(0)
    bert_embedding = BertEmbedding(ctx=ctx)

Example of using the large pre-trained BERT model from Google

.. code-block:: python

    from bert.embedding import BertEmbedding

    bert_embedding = BertEmbedding(model='bert_24_1024_16', dataset_name='book_corpus_wiki_en_cased')

Example outputs:

.. code-block:: python

    first_sentence = result[0]

    first_sentence[0]
    # array([-0.835946  , -0.4605566 , -0.95620036, ..., -0.95608854,
    #       -0.6258104 ,  0.7697007 ], dtype=float32)
    first_sentence[0].shape
    # (768,)

    first_sentence[1]
    # ['we', 'introduce', 'a', 'new', 'language', 'representation', 'model', 'called', 'bert', ',', 'which', 'stands', 'for', 'bidirectional', 'encoder', 'representations', 'from', 'transformers']
    len(first_sentence[1])
    # 18


    len(first_sentence[2])
    # 18
    first_token_in_first_sentence = first_sentence[2]
    first_token_in_first_sentence[0]
    # array([ 0.4805648 ,  0.18369392, -0.28554988, ..., -0.01961522,
    #        1.0207764 , -0.67167974], dtype=float32)
    first_token_in_first_sentence[0].shape
    # (768,)

Command line interface
++++++++++++++++++++++

.. code-block:: shell

    python bert_embedding/bert.py --sentences "GluonNLP is a toolkit that enables easy text preprocessing, datasets loading and neural models building to help you speed up your Natural Language Processing (NLP) research."
    Text: GluonNLP is a toolkit that enables easy text preprocessing, datasets loading and neural models building to help you speed up your Natural Language Processing (NLP) research.
    Sentence embedding: [-0.6098857  -0.1458175  -0.2767048  ... -0.42009002 -0.40388978
  0.2774383 ]
    Tokens embedding: [array([-0.11881411, -0.59530115,  0.627092  , ...,  0.00648153,
       -0.03886228,  0.03406909], dtype=float32), array([-0.7995638 , -0.6540758 , -0.00521846, ..., -0.42272145,
       -0.5787281 ,  0.7021201 ], dtype=float32), array([-0.7406778 , -0.80276626,  0.3931962 , ..., -0.49068323,
       -0.58128357,  0.6811132 ], dtype=float32), array([-0.43287313, -1.0018158 ,  0.79617643, ..., -0.26877284,
       -0.621779  , -0.2731115 ], dtype=float32), array([-0.8515188 , -0.74098676,  0.4427735 , ..., -0.41267148,
       -0.64225197,  0.3949393 ], dtype=float32), array([-0.86652845, -0.27746758,  0.8806506 , ..., -0.87452525,
       -0.9551989 , -0.0786318 ], dtype=float32), array([-1.0987284 , -0.36603633,  0.2826037 , ..., -0.33794224,
       -0.55210876, -0.09221527], dtype=float32), array([-0.3483025 ,  0.401534  ,  0.9361341 , ..., -0.29747447,
       -0.49559578, -0.08878893], dtype=float32), array([-0.65626   , -0.14857645,  0.29733548, ..., -0.15890433,
       -0.45487815, -0.28494897], dtype=float32), array([-0.1983894 ,  0.67196256,  0.7867421 , ..., -0.7990434 ,
        0.05860569, -0.26884627], dtype=float32), array([-0.3775159 , -0.00590206,  0.5240432 , ..., -0.26754653,
       -0.37806216,  0.23336883], dtype=float32), array([ 0.1876977 ,  0.30165672,  0.47167772, ..., -0.43823618,
       -0.42823148, -0.48873612], dtype=float32), array([-0.6576557 , -0.09822252,  0.1121515 , ..., -0.21743725,
       -0.1820574 , -0.16115054], dtype=float32)]
