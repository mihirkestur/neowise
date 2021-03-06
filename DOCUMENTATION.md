## *neowise* Documentation

### Steps to train your own Neural Network using *neowise*

 1. Install and `import neowise as nw`

 2. Get your data and pre-process it. Your `data` should be in the dimensions as `(number_of_examples, number_of_features)` and `labels` should have `(number_of_output_units, number_of examples)` as its dimensions. 
This is a must, any changes here would raise errors!

3. Create a model by calling `model = nw.Model(your_train_data, your_train_labels, your_test_data, your_test_labels, your_crossval_data, your_crossval_labels)` If you do not have Cross Validation data, enter `None` for the last two arguments.

4. Add layers to your model by `model.add(layer_name,num_inputs,num_outputs,activation_function,dropout)`, where you give a unique name to each of your layers so that you know what type of layer it is. Example for `dense` layer, if it is your first layer, name it `dense1`. Enter the number of inputs to that layer, in `num_inputs` and number of units for that layer in `num_outputs`.
For activation_function use *any of the following supported activation functions* **["relu", "sigmoid", "tanh", "softmax", "sine"]**. 
To prevent overflows and nans, we suggest that if you use a softmax classifier, to set the activation of the previous layer of the output layer as **"tanh"** as it squishes values between -1 and 1, thus preventing catastrophe. If you want to use Dropout, set the `dropout` anywhere between 0 and 1. Else, the default value is taken as 1, i.e no Dropout.

5. Just to be sure of your architecture and to know the amount of parameters that'll be trained call `model.summary()` which uses prettytable to print out a summary of your architecture.

6. Train your model using `model.fit(your_train_data, your_train_labels, learning_rate, number_of_iterations, optimizer, problem_type, mini_batch_size, regularization_type, lambda, learning_rate_decay)`, where you enter your training data, choose the learning rate, set the number of iterations to train for, choose which type of optimizer you want from **["GD" for Gradient Descent, "Momentum" for Gradient Descent using Momentum, "RMSprop" for Root Mean Square Propagation, "Adam" for Adaptive Moment Estimation]** If you want to train using ***Batch Gradient Descent***, choose **"GD"** as `optimizer` and set the `mini_batch_size` to the total number of examples in your training data and if you want to train using ***Stochastic Gradient Descent***, choose **"GD"** as `optimizer` and set `mini_batch_size` to 1. For `problem_type` choose any of the currently supported tasks **["Binary" for Binary Classification Tasks, "Multi" for Multi Class Classification Tasks]** Set `mini_batch_size` to the size you want each of your mini batches to be and be sure that this value is less than the total number of examples you have. If you want to use L1 or L2 regularization choose from **["L1" for L1 Regularization and "L2" for L2 Regularization]** and set the regularization parameter `lambda`. If you want your `learning_rate` to not be constant and be decreasing as the training progresses, set `alpha_decay` to True

7. Test the model on your test data by calling `model.test(your_test_data, your_test_labels, problem_type)` on your training data and set `problem_type` as you did for `model.fit`. This displays a prettytable with precision, recall and f1 scores and its accuracy on the test data.

8. For plotting the costs and accuracy vs number of iterations, call `model.plot(type_function, animate, directory, frequency)` and set `type_function` to **"Cost"** if you want to plot costs vs number of iterations and **"Accuracy"** for accuracy vs number of iterations. If you want to create animated graphs, set `animate` to True and specify the directory in which you want to save the plots in `directory` and set the frequency with which the graphs should update in `frequency`, then feed those images to a GIF creator to create animated plots.

9. To save the model, call `model.save_model(file_name)` and specify the directory in which you want to save the model with the name of the model with the extension .h5 in `filename`

10. To load a previously saved model, create a new model be calling `saved_model =  nw.Model(your_train_data, your_train_labels, your_test_data, your_test_labels, your_crossval_data, your_crossval_labels)`, where these are the same data on which model was trained on. `Call saved_model.load_model(file_name)`  to load the model from the directory specified in `file_name`

11. These are the functionalities that ***neowise*** offers. For detailed doc_strings visit [Source Code](https://github.com/pranavsastry/neowise/tree/master/neowise/neowise) to find more about the project!
