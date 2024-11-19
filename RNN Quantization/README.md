### README: RNN Quantization Example

This project demonstrates how to create, train, and quantize a simple RNN model using TensorFlow/Keras. The goal is to optimize the model for deployment by converting it into TensorFlow Lite format with 8-bit quantization. Along the way, we encountered and resolved an error related to TensorFlow Lite conversion.

---

### Project Steps

1. **Generate Dataset**  
   Randomly generate sequences of numbers (`x`) and their sums (`y`) as the target values.

2. **Define the Model**  
   The model consists of:
   - A `SimpleRNN` layer with 64 units.
   - A `Dense` layer with 1 unit for regression.

3. **Train the Model**  
   Use the Adam optimizer and train the model for 20 epochs with a batch size of 32.

4. **Quantize the Model**  
   Convert the trained model to TensorFlow Lite format with 8-bit quantization using post-training quantization.

---

### Error Encountered

While converting the model to TensorFlow Lite, we encountered this error:

```
ConverterError: Variable constant folding is failed. Please consider enabling `experimental_enable_resource_variables` flag in the TFLite converter object. 
For example, converter.experimental_enable_resource_variables = True.
```

The error indicates that the `SimpleRNN` layer's internal operations (like `TensorListReserve`) are not directly supported by TensorFlow Lite's built-in ops. We fixed this by enabling TensorFlow ops during the conversion process.

---

### How We Fixed It

We adjusted the TFLite conversion process to include TensorFlow-specific operations by adding:

```python
converter.target_spec.supported_ops = [
    tf.lite.OpsSet.TFLITE_BUILTINS,  # TFLite native ops
    tf.lite.OpsSet.SELECT_TF_OPS     # TensorFlow ops
]
converter._experimental_lower_tensor_list_ops = False
```

This allows the conversion to handle operations that aren’t natively supported by TFLite.

---

### Requirements

- Python 3.x
- TensorFlow 2.x
- Numpy

Install dependencies using:
```bash
pip install tensorflow numpy
```

---

### Running the Code

1. Train the RNN model:
   ```bash
   python train_model.py
   ```

2. Convert the model to TensorFlow Lite:
   ```bash
   python convert_to_tflite.py
   ```

3. The quantized model will be saved as `quantized_rnn_model.tflite`.

---
