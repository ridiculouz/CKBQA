# CKBQA

>**Update June 2nd, 2021**:  add BibTex.

>**Update May 6th, 2021**:  our [paper](zhang2021namer.pdf) will appear at [NAACL 2021 System Demonstration track](https://www.aclweb.org/anthology/2021.naacl-demos.3/), please check it out for more details on data annotations and evaluations.

## Introduction

This repository contains a Chinese KBQA dataset expanded from CCKS CKBQA Competition Dataset. We also provide a novel framework based on these additional annotations in a [paper](zhang2021namer.pdf), an online [demo](http://kbqademo.gstore.cn/) of such KBQA system is available, have fun to check it out!


## Citation & Trouble Shooting

Please contact us via *{zhangminhao, ry_zhang}@pku.edu.cn* if you have any questions or kindly cite the following paper if you find this resource helpful.

```
@inproceedings{zhang-etal-2021-namer,
    title = "{NAMER}: A Node-Based Multitasking Framework for Multi-Hop Knowledge Base Question Answering",
    author = "Zhang, Minhao  and
      Zhang, Ruoyu  and
      Zou, Lei  and
      Lin, Yinnian  and
      Hu, Sen",
    booktitle = "Proceedings of the 2021 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies: Demonstrations",
    month = jun,
    year = "2021",
    address = "Online",
    publisher = "Association for Computational Linguistics",
    url = "https://www.aclweb.org/anthology/2021.naacl-demos.3",
    pages = "18--25",
}
```

## Data Format

The validation dataset and training dataset are provided in this repository in json format. Each entry contains a question, its question id, its corresponding gold SPARQL, and the **struct** of the SPARQL. We define variable, entity, literal and type in SPARQL as **node**. The struct shows triples' **relation**s, the head and tail nodes of triples and their **mentions**, including start and end offsets. Besides, **filter** information is also contained in the struct.  

Here are two examples:

**SPARQL:** select ?x where { <微软> <主要软件产品> ?x. }

**Struct:** {
            "selected_variable": {
                "node": "?x",
                "type": "variable",
                "mention": {
                    "start_offset": 7,
                    "end_offset": 11,
                    "natural_language": "软件产品"
                }
            },
            "triple": [
                {
                    "head": {
                        "node": "<微软>",
                        "type": "entity",
                        "mention": {
                            "start_offset": 0,
                            "end_offset": 4,
                            "natural_language": "微软公司"
                        }
                    },
                    "relation": "<主要软件产品>",
                    "tail": {
                        "node": "?x",
                        "type": "variable",
                        "mention": {
                            "start_offset": 7,
                            "end_offset": 11,
                            "natural_language": "软件产品"
                        }
                    }
                }
            ],
            "filter": []
        }
        
**SPARQL:** select ?y where { <最后的晚餐_（达·芬奇画作）> <作者> ?x. ?x <职业> ?z. ?y <职业> ?z. filter(?y!=?x). }

**Struct:** {
            "selected_variable": {
                "node": "?y",
                "type": "variable",
                "mention": {
                    "start_offset": 17,
                    "end_offset": 18,
                    "natural_language": "人"
                }
            },
            "triple": [
                {
                    "head": {
                        "node": "<最后的晚餐_（达·芬奇画作）>",
                        "type": "entity",
                        "mention": {
                            "start_offset": 1,
                            "end_offset": 8,
                            "natural_language": "《最后的晚餐》"
                        }
                    },
                    "relation": "<作者>",
                    "tail": {
                        "node": "?x",
                        "type": "variable",
                        "mention": {
                            "start_offset": 9,
                            "end_offset": 11,
                            "natural_language": "作者"
                        }
                    }
                },
                {
                    "head": {
                        "node": "?x",
                        "type": "variable",
                        "mention": {
                            "start_offset": 9,
                            "end_offset": 11,
                            "natural_language": "作者"
                        }
                    },
                    "relation": "<职业>",
                    "tail": {
                        "node": "?z",
                        "type": "variable",
                        "mention": {
                            "start_offset": 14,
                            "end_offset": 16,
                            "natural_language": "职业"
                        }
                    }
                },
                {
                    "head": {
                        "node": "?y",
                        "type": "variable",
                        "mention": {
                            "start_offset": 17,
                            "end_offset": 18,
                            "natural_language": "人"
                        }
                    },
                    "relation": "<职业>",
                    "tail": {
                        "node": "?z",
                        "type": "variable",
                        "mention": {
                            "start_offset": 14,
                            "end_offset": 16,
                            "natural_language": "职业"
                        }
                    }
                }
            ],
            "filter": [
                "filter(?y!=?x)"
            ]
        }
