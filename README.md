# DeepPicar
DeepPicar is a low-cost autonomous vehcile platform that can be used for 
researching performance requirements for self-driving cars.

## Driving DeepPicar
For manual control:

	$ python picar-mini-kbd-drv8835.py

The controls are as follows:
* 'a': drive the car forward
* 'z': drive the car backward
* 's': stop the car
* 'j': turn the car left
* 'k': center the car
* 'l': turn the car right
* 't': toggle video view
* 'r': record video
    
For autonomous control:

	$ python picar-mini-dnn-drv8835.py
    
## Model Training
Change model (folder) name:

	save_dir = os.path.abspath('...') #Replace ... with a name for the model
    
Change if normal category is to be used:

	use_normal_category = True #True = equally select center/curve images, 
False = no equal selection

Select epochs to be used for training and validation in the params.py file:

	epochs['train'] = [...] #Replace ... with integer values used to 
represent epochs  
	epochs['val'] = [...] #Replace ... with integer values used to 
represent epochs
    
The model can then be trained by running:

	$ python train.py
    
## Embedded Computing Platform Evaluation
By default, the platforms are tested over epoch 6 (out-video-6.avi), but 
the epochs processed can be changed by altering epoch_ids in test-model.py:

	epoch_ids = [...] #Replace ... with all epochs to be processed
	
Also, epochs can be processed more than once (i.e. epoch_ids = [6,6] would 
have the platform process epoch 6 twice).

The number of frames processed can be increased/decreased as well by 
changing:

	NFRAMES = _ #Replace _ with the total number of frames to process

### Evaluation Scripts

For convenience, the platforms can be fully tested by running the following 
scripts:

Raspberry Pi 3 / Intel UP board:

	$ ./test-model_timings.sh # Run all multicore and multimodel tests
	$ ./benchmark_timings.sh # Run all synthetic benchmark/co-runner tests 
w/ perf information
	$ ./benchmark_timings_noperf.sh # Same as benchmark_timings.sh but 
doesn't measure perf information
	
NVIDIA Jetson TX2:

	$ ./test-model_timings_x2.sh # Run all multicore and multimodel tests 
while using the GPU
	$ ./test-model_timings_x2_cpu.sh # Run all multicore and multimodel 
tests while using the CPU only
	$ ./benchmark_timings_x2.sh # Run all synthetic benchmark/co-runner 
tests while utilizing the GPU
	$ ./benchmark_timings_x2_cpu.sh # Run all synthetic benchmark/co-runner 
tests while only using the CPU
    
## Additional Information
Please refer to 
[PicarMini.md](https://github.com/heechul/picar/blob/picar-mini-v2.0-release/
PicarMini.md) for more detailed explanations/instructions.