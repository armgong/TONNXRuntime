<p align="center">
  <img style="width :50%"src="https://onnxruntime.ai/images/svg/ONNX-Runtime-logo-white.svg" alt="ONNXRuntime for Freepascal / Delphi"</img>
</p>

## Microsoft ONNXRuntime AI and Machine Learning Library for Freepascal / Delphi

## Introduction
This is an implementation of Microsoft's [Open Neural Network Exchange](https://www.onnxruntime.ai/about.html) (ONNXRuntime) for [Freepascal 🐾](https://www.lazarus-ide.org) and [Delphi ⚔️](https://www.embarcadero.com/products/delphi/starter)

ONNXRuntime libraries comes shipped with most of modern Windows releases after **Windows 8**, as of the time this is written version 1.13.1 the most recent release, it can be installed on **MacOS** and most of **Linux** releases, for development and updates please visit [ONNXRuntime Github Page](https://github.com/microsoft/onnxruntime/).

## How to install libraries
##### Windows
  
  `onnxruntime.dll` is already shipped with windows, you can find it in `%WINDIR%\SysWOW64\onnxruntime.dll` or`%WINDIR%\System32\onnxruntime.dll` 

##### MacOS and linux
  
  check https://github.com/microsoft/onnxruntime/releases



## Usage

From you **Lazarus** or **Delphi** project at the header of the pascal unit include the files
  ```
  unit formUnit;
  {$h+}
  
  interface
  uses onnxruntime_pas_api, onnxruntime, Classes etc... ;
  ```
##### Load a Model
  ```
  var 
    session : TORTSession;
  begin
    session := TORTSession.Create("./mymodel/filname.onnx"); 
  { 
  *****************************************************************
      Check your model requirements for input/output 
      names and value dimensions before preparing the inputs.
      to explorer the model before preparing use :
        session.GetInputCount and session.GetOutputCount
        session.GetInputName and session.GetOutputName
        session.GetInputTypeInfo and session.GetOutputTypeInfo
   ****************************************************************
  }
```    

##### Prepare an input tensor with the desired shape using `TORTTensor<type>` and your inputs using `TORTNameValueList`

```
var 
  x,y:integer;
  data : array of array of single;
  inTensor : TORTTensor<single> ; 
  inputs : TORTNameValueList  ;
begin
  // assuming the model input name is 'image' and the tensor shape is [width, height]
  inTensor := TORTTensor<single>.Create([width, height{, depth ,etc...}]);
  for y:=0 to tensor.shape[1] do
      for x:=0 to tensor.shape[0] do 
          tensor.index2[x, y]:= data[x, y];  // your float values
  inputs['image'] := inTensor;        
```

##### Inferance

```
  var
    myDetection : array of single;
    i:integer;
    outputs : TORTNameValueList;
    outTensor : TORTTensor<single>
  bagin 
      outputs   := session.run(inputs);
      outTensor := outputs['result']
     
      for i:=0 to outTensor.shape[0] do
        myDetection[i] := outTensor.index1[i]
```

##### Training

###### More examples Coming soon..
   

#### More information about ONNXRuntime API

* Check the [Faster RCNN10 example](/examples/FasterRCNN) folder
  Download `FasterRCNN10.onnx [here](https://github.com/onnx/models/tree/main/vision/object_detection_segmentation/faster-rcnn/model)
* Check [ONNXRuntime API Documents](https://onnxruntime.ai/docs/api/)
  
---  
#### Contributions and suggestions are most welcome.
