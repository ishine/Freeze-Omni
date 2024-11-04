# Freeze-Omni: A Smart and Low Latency Speech-to-speech Dialogue Model with Frozen LLM


<p align="center">
    <img src="./assets/logo.png" width="100%" height="100%">
</p>

<font size=7><div align='center' > [[🍎 Project Page](https://freeze-omni.github.io/)] [[📖 arXiv Paper](https://arxiv.org/abs/2411.00774)]</div></font>


---

## 🔥 News
* **`2024.11.4`** 🌟 We are very proud to launch Freeze-Omni, a speech-to-speech dialogue model
with both low-latency and high intelligence! We have submitted the open-source code, yet it is under review internally. We are moving the process forward as quickly as possible, stay tuned!


## 👀 Freeze-Omni Overview
Freeze-Omni is a speech-to-speech dialogue model, exhibiting the characteristic of being "**smart**" as it is constructed upon a "**frozen**" text-modality LLM. This enables it to keep the original intelligence of the LLM backbone, without being affected by the forgetting problem induced by the fine-tuning process for integration of the speech modality. Specifically, Freeze-Omni contains a speech encoder that supports streaming speech input and a speech decoder that generates streaming output speech. **Three key strategies** are adopted to implement the speech-to-speech dialogue system::

- **Chunk-wise Streaming Input**. Freeze-Omni has a speech encoder supporting chunk-wise streaming input speech features to obtain a fast response to input. A 3-stage training strategy can help it keep strong acoustic robustness.

- **AR-base Speech Output**. Freeze-Omni has an AR speech decoder based on a single codebook, which can achieve low-latency speech output in streaming. A prefix tuning method is used so that training on only a small amount of Q&A data can achieve the ability to produce high-quality speech synthesis.

- **Chunk-level State Prediction**. Freeze-Omni adds a classification layer after the last layer of the backbone LLM to predict different states. These states will determine whether or not the LLM interrupts the user to achieve a duplex dialogue for the user and the bot.

<p align="center">
    <img src="./assets/overview.png" width="88%" height="88%">
</p>

Besides we implement a Model as a Server strategy. We first started several models simultaneously and regarded them as a server. Then, when a user's VAD was triggered, the speech would be sent to the server in the form of chunks, and the server would be responsible for scheduling which idle model should respond to the current chunk. Since we separated all the kv-cache and CNN cache of the speech encoder and LLM during the inference process, the server only needs to save the inference cache for each user. In this way, any model in the server could respond to any chunk of any user, and there was no need to specify which model was used as a monitor or a generator.



## 📈 Experimental Results
- **Evaluation of speech understanding through ASR tasks, using CER(%) and WER(%).**.

<p align="center">
    <img src="./assets/language_eval2.png" width="68%" height="50%">
</p>


- **Evaluation of output speech quality on different top-k of AR decoder by using CER(%).**

<p align="center">
    <img src="./assets/audio_eval.jpg" width="96%" height="96%">
</p>

- **Evaluation of spoken question answering on accuracy(%).**

<p align="center">
    <img src="./assets/visual_eval.jpg" width="100%" height="100%">
</p>

- **Analysis of end-to-end latency for different parts.**

<p align="center">
    <img src="./assets/visual_eval.jpg" width="100%" height="100%">
</p>


## ✒️ Citation

If you find our work helpful for your research, please consider citing our work.   

```bibtex
@article{xiong2024freeze,
  title={Freeze-Omni: A Smart and Low Latency Speech-to-speech Dialogue Model with Frozen LLM},
  author={Xiong Wang and Yangze Li and Chaoyou Fu and Lei Xie and Ke Li and Xing Sun and Long Ma},
  journal={arXiv preprint arXiv:2411.00774},
  year={2024}
}
```


## 📜 Related Works

Explore our related researches:
-  **[VITA]** [Towards Open-Source Interactive Omni Multimodal LLM](https://github.com/VITA-MLLM/VITA)
-  **[Awesome-MLLM]** [A Survey on Multimodal Large Language Models](https://github.com/BradyFU/Awesome-Multimodal-Large-Language-Models)
-  **[MME]** [MME: A Comprehensive Evaluation Benchmark for Multimodal Large Language Models](https://github.com/BradyFU/Awesome-Multimodal-Large-Language-Models/tree/Evaluation)
-  **[Video-MME]** [Video-MME: The First-Ever Comprehensive Evaluation Benchmark of Multi-modal LLMs in Video Analysis](https://github.com/BradyFU/Video-MME) 
