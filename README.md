# Clause Extraction

An implementation of algorithm described in paper
[_L. Zhang, H. Zhu, S. Brahma, and Y. Li, “Small but Mighty: New Benchmarks for
Split and Rephrase,” 2020._](https://arxiv.org/abs/2009.08560)

## Usage

```txt
split.py [-h] [--udpipe_model_path UDPIPE_MODEL_PATH] [--srl_model_path SRL_MODEL_PATH] [--sep SEP] --input INPUT --output OUTPUT

optional arguments:
  -h, --help            show this help message and exit
  --udpipe_model_path UDPIPE_MODEL_PATH
                        Path to the UDPipe model.
  --srl_model_path SRL_MODEL_PATH
                        Path to the AllenNLP semantic role labeling model.
  --sep SEP             Clause separator used in the output file.
  --input INPUT         Input file.
  --output OUTPUT       Output file.
```

## The Algorithm

The description of the algorithm from the paper (Appendix A):

> Given a complex sentence, the model runs the following processes once each.
>
> **Wh Handling**
>
> Using semantic role labeling, the model looks for a
> Relational Argument (R-ARG), and the Subject Argument (asserted to be the ARG
> preceding the R-ARG). Then, a split is made with the Relational Argument
> replaced by the Subject Argument.
>
> **Conjunction Handling**
>
> The model looks for the word “and”. Using semantic role labeling, if the word
> following “and” is an argument (ARG), assert that “and” is followed by a
> sentence, and a split is made. Or, if the word following “and” is a verb (V),
> the model asserts the Subject Argument to be the ARG preceding the V; a split
> is made with “and” replaced by the Subject Argument.
>
> **Insertion Handling**
>
> Using dependency parsing, the model looks for a node
> with type participle modifier, relative clause modifier, prepositional
> modifier, adjective modifier, or appositional modifier. The clause with the
> node as the root is extracted, prepended with the subject, and split as a new
> simple sentence. The rest of the original complex sentence is split as
> another new simple sentence.

