# Tiny YOLO v3 ZYNQ

## What is this project about?

FPGA implementation of YOLOv3-tiny 

- Scalable & parameterizable

- Latency-driven

- Tailored for FPGA device with limited resources

Latency and resource analytical models 
- Hardware and software latency
- DSP and BRAM utilization

Design Space Exploration to identify the Pareto-optimal design point on Zedboard

## To cite our work
Our paper is accepted by ARC2020 (https://arcoresearch.com/arc2020/)

@inproceedings{yu2020parameterisable,
  title={A Parameterisable FPGA-Tailored Architecture for YOLOv3-Tiny},
  author={Yu, Zhewen and Bouganis, Christos-Savvas},
  booktitle={Applied Reconfigurable Computing. Architectures, Tools, and Applications. ARC 2020. Lecture Notes in Computer Science, vol 12083},
  pages={330-344},
  year={2020},
  month={03},
  publisher={Springer, Cham},
  url={https://doi.org/10.1007/978-3-030-44534-8_25}
}

## Navigate inside the project
/code

main codebase including "templates" (managed by the script) and a design example (with bitfile and sdk, ready for deployment on Zedboard)

/data

weights and test data

/document

include the paper (recommend read first) and thesis (more detailed)

/model

code used for analytical models and design space exploration

/scripts

entry point for the automated framework

/tools

some tools used for helping the test, not important

## How to use the automated flow

Check environment
- ubuntu 16.04 LTS 
- Vivado v2019.1
- python 3.5.2
- gcc 5.4.0

Set target FPGA, clock and resource constraints by

Edit scripts/run_all.py

*Currently, the following FPGA (on Zedboard) has been tested. But the design should work for other Xilinx Zynq devices*
```
device = "xc7z020-clg484-1"
clk_ns = "10"
```

Edit model/main.cpp

*You have to specify resources constriants. The script is not able to infer resources available from the device you previously chose.*
```
#define DEFAULT_MAX_DSP (220) // zynq7020
#define DEFAULT_MAX_BRAM_18k (280) // zynq7020
#define DEFAULT_MAX_ULTILISATION (0.9)  // usually won't use 100% resources
```

Run scripts/run_all.py

2000 years later...

You will have the Vivado SDK GUI

Create an application project, add files from code/sdk (Notice if you have changed the resource constraints, you need to manually update the folding factors in make_layer_group)

Increase the heap size as code/sdk/src/lscript.ld shows

The latency of the inference shall be printed which indicates the system is working

If you want to get the bounding boxes, please refer to https://github.com/pjreddie/darknet for more details on converting the network outputs to bbox

 ## Contact me

 you can either create an issue or just drop me an email (zhewen.yu18@imperial.ac.uk)

