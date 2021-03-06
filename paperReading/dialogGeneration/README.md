# overview
some papers of dialogue generation for chat(including related methods)
# Survey
* [Challenges in Building Intelligent Open-domain Dialog Systems] [[paper](https://arxiv.org/pdf/1905.05709.pdf "MINLIE HUANG, XIAOYAN ZHU, JIANFENG GAO")](2019) `chatbot`
* [Neural Approaches to Conversational AI Question Answering, Task-Oriented Dialogue and Chatbots: A Unified View] [[paper](https://arxiv.org/pdf/1809.08267v1.pdf "Jianfeng Gao, Michel Galley, Lihong Li")](2018) `QA, task-dialogue, chatbot`
* [Teaching Machines to Converse] [[paper](https://github.com/jiweil/Jiwei-Thesis/blob/master/thesis.pdf "Jiwei Li")](2018) `chatbot`
* [A Survey on Dialogue Systems: Recent Advances and New Frontiers] [[paper](https://arxiv.org/pdf/1711.01731.pdf "Hongshen Chen, Xiaorui Liu, Dawei Yin, Jiliang Tang")](2017) `task-dialogue, chatbot`
* [Sequence-to-Sequence Learning for End-to-End Dialogue Systems] [[paper](https://www.researchgate.net/publication/313374979_Sequence-to-Sequence_Learning_for_End-to-End_Dialogue_Systems "Jordy Van Landeghem")](2017) `chatbot`
# papers
## ICLR
* [Auto-Encoding Variational Bayes] [[paper](https://arxiv.org/pdf/1312.6114.pdf "Diederik P. Kingma and Max Welling")](2014) `VAE`
* [NEURAL MACHINE TRANSLATION BY JOINTLY LEARNING TO ALIGN AND TRANSLATE] [[paper](https://arxiv.org/pdf/1409.0473.pdf "Dzmitry Bahdanau, KyungHyun Cho, Yoshua Bengio")](2015) `Attention`
## NeurIPS
* [Sequence to Sequence Learning with Neural Networks] [[paper](https://arxiv.org/pdf/1409.3215.pdf "Ilya Sutskever, Oriol Vinyals, Quoc V. Le")](2014) `seq2seq`
* [A Recurrent Latent Variable Model for Sequential Data] [[paper](https://papers.nips.cc/paper/5653-a-recurrent-latent-variable-model-for-sequential-data.pdf "Junyoung Chung, Kyle Kastner, Laurent Dinh, Kratarth Goel, Aaron Courville, Yoshua Bengio")](2015) `VRNN`
## ICML
* [Toward Controlled Generation of Text] [[paper](https://arxiv.org/pdf/1703.00955.pdf "Zhiting Hu, Zichao Yang, Xiaodan Liang, Ruslan Salakhutdinov, Eric P. Xing")](2017)
## ACL
* [A Conditional Variational Framework for Dialog Generation] [[paper](https://arxiv.org/pdf/1705.00316.pdf "Xiaoyu Shen, Hui Su, Yanran Li, Wenjie Li, Shuzi Niu, Yang Zhao, Akiko Aizawa and Guoping Long")](2017) `SPHRED` `Conditional Variation for dialogue`
* [Learning Discourse-level Diversity for Neural Dialog Models using Conditional Variational Autoencoders] [[paper](https://arxiv.org/pdf/1703.10960.pdf "Tiancheng Zhao, Ran Zhao and Maxine Eskenazi")](2017)
* [MOJITALK: Generating Emotional Responses at Scale] [[paper](https://arxiv.org/pdf/1711.04090.pdf "Xianda Zhou and William Yang Wang")](2018) `control dialogue by emoji labels`
* [Generating Informative Responses with Controlled Sentence Function] [[paper](https://www.aclweb.org/anthology/P18-1139 "Pei Ke, Jian Guan, Minlie Huang, Xiaoyan Zhu")](2018)
* [Unsupervised Discrete Sentence Representation Learning for Interpretable Neural Dialog Generation] [[paper](https://arxiv.org/pdf/1804.08069.pdf "Tiancheng Zhao, Kyusong Lee and Maxine Eskenazi")](2018)
* [Learning to Control the Specificity in Neural Response Generation] [[paper](https://www.aclweb.org/anthology/P18-1102 "Ruqing Zhang, Jiafeng Guo, Yixing Fan, Yanyan Lan, Jun Xu and Xueqi Cheng")](2018) `SC-Seq2Seq:seq2seq + Gaussian Kernel layer(approximate a float label between 0 to 1)` `control dialogue by specific label` `make dialogue more interesting`
* [Generating Responses with a Specific Emotion in Dialog] [[paper](https://www.aclweb.org/anthology/P19-1359 "Zhenqiao Song, Xiaoqing Zheng, Lu Liu, Mu Xu and Xuanjing Huang ")](2019) `EmoDS:seq2seq + lexicon-based attention + emotion classification` `control dialogue by emotion lexicon` `semi-supervised emotion lexicon construction`
## NAACL
* [A Neural Network Approach to Context-Sensitive Generation of Conversational Responses] [[paper](http://export.arxiv.org/pdf/1506.06714 "Alessandro Sordoni, Michel Galley, Michael Auli, Chris Brockett, Yangfeng Ji, Margaret Mitchell, Jian-Yun Nie, Jianfeng Gao, Bill Dolan")](2015) `vanilla RNN for dialogue`
* [Automatic Dialogue Generation with Expressed Emotions] [[paper](https://www.aclweb.org/anthology/N18-2008.pdf "Chenyang Huang, Osmar R. Zaiane, Amine Trabelsi, Nouha Dziri")](2018) `three simple emotion chating(en) methods`
* [Affect-Driven Dialog Generation] [[paper](https://www.aclweb.org/anthology/N19-1374.pdf "Pierre Colombo, Wojciech Witon, Ashutosh Modi, James Kennedy, Mubbasir Kapadia")](2019) `EMOTICONS:seq2seq + loss(word-level emotion VAD) + re-rank(MMI-bidi and emotion VAD)` `control dialogue by emotion label(VAD)`
## EMNLP
* [Learning Phrase Representations using RNN Encoder–Decoder for Statistical Machine Translation] [[paper](https://arxiv.org/pdf/1406.1078.pdf "Kyunghyun Cho, Bart van Merrienboer, Caglar Gulcehre, Dzmitry Bahdanau, Fethi Bougares, Holger Schwenk, Yoshua Bengio")](2014) `encoder-decoder` `GRU`
* [Adversarial Learning for Neural Dialogue Generation] [[paper](https://arxiv.org/pdf/1701.06547.pdf "Jiwei Li, Will Monroe, Tianlin Shi, Sebastien Jean, Alan Ritter and Dan Jurafsky")](2017)
## AAAI
* [Building End-To-End Dialogue Systems Using Generative Hierarchical Neural Network Models] [[paper](https://arxiv.org/pdf/1507.04808.pdf "Iulian V. Serban, Alessandro Sordoni, Yoshua Bengio, Aaron Courville and Joelle Pineau")](2016) `HRED for dialogue`
* [A Hierarchical Latent Variable Encoder-Decoder Model for Generating Dialogues] [[paper](https://arxiv.org/pdf/1605.06069.pdf "Iulian V. Serban, Alessandro Sordoni, Ryan Lowe, Laurent Charlin, Joelle Pineau, Aaron Courville and Yoshua Bengio")](2017) `VHRED`
* [Improving Variational Encoder-Decoders in Dialogue Generation] [[paper](https://arxiv.org/pdf/1802.02032.pdf "Xiaoyu Shen, Hui Su, Shuzi Niu, Vera Demberg")](2018) `about KL-vanishing`
* [Emotional Chatting Machine: Emotional Conversation Generation with Internal and External Memory] [[paper](https://www.aaai.org/ocs/index.php/AAAI/AAAI18/paper/view/16455/15753 "Hao Zhou, Minlie Huang, Tianyang Zhang, Xiaoyan Zhu, Bing Liu")](2018) `ECM:seq2seq + internal memory + external memory(emotion lexicon)` `control dialogue by emotion label`
## CIKM
* [A Hierarchical Recurrent Encoder-Decoder for Generative Context-Aware Query Suggestion] [[paper](https://arxiv.org/pdf/1507.02221.pdf "Alessandro Sordoni, Yoshua Bengio, Hossein Vahabi, Christina Lioma, Jakob G.Simonsen, Jian-Yun Nie")](2015)`HRED`
## arXiv
* [How NOT To Evaluate Your Dialogue System: An Empirical Study of Unsupervised Evaluation Metrics for Dialogue Response Generation] [[paper](https://arxiv.org/pdf/1603.08023.pdf "Chia-Wei Liu, Ryan Lowe, Iulian V. Serban, Michael Noseworthy, Laurent Charlin, Joelle Pineau")](2017)`Evaluate Dialogue`
