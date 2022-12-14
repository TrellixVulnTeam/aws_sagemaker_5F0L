=======================================
SageMaker PyTorch Estimators and Models
=======================================

With PyTorch Estimators and Models, you can train and host PyTorch models on Amazon SageMaker.

Supported versions of PyTorch: ``0.4.0``, ``1.0.0``, ``1.1.0``, ``1.2.0``.

We recommend that you use the latest supported version, because that's where we focus most of our development efforts.

You can visit the PyTorch repository at https://github.com/pytorch/pytorch.

For information about using PyTorch with the SageMaker Python SDK, see https://sagemaker.readthedocs.io/en/stable/using_pytorch.html.

PyTorch Training Examples
-------------------------

Amazon provides several example Jupyter notebooks that demonstrate end-to-end training on Amazon SageMaker using PyTorch.
Please refer to:

https://github.com/awslabs/amazon-sagemaker-examples/tree/master/sagemaker-python-sdk

These are also available in SageMaker Notebook Instance hosted Jupyter notebooks under the sample notebooks folder.


SageMaker PyTorch Docker Containers
-----------------------------------

When training and deploying training scripts, SageMaker runs your Python script in a Docker container with several
libraries installed. When creating the Estimator and calling deploy to create the SageMaker Endpoint, you can control
the environment your script runs in.

SageMaker runs PyTorch Estimator scripts in either Python 2 or Python 3. You can select the Python version by
passing a ``py_version`` keyword arg to the PyTorch Estimator constructor. Setting this to `py3` (the default) will cause your
training script to be run on Python 3.5. Setting this to `py2` will cause your training script to be run on Python 2.7
This Python version applies to both the Training Job, created by fit, and the Endpoint, created by deploy.

The PyTorch Docker images have the following dependencies installed:

+-----------------------------+---------------+-------------------+-------------------+
| Dependencies                | pytorch 0.4.0 | pytorch 1.0.0     | pytorch 1.1.0     |
+-----------------------------+---------------+-------------------+-------------------+
| boto3                       | >=1.7.35      | >=1.9.11          | 1.9.82            |
+-----------------------------+---------------+-------------------+-------------------+
| botocore                    | >=1.10.35     | >=1.12.11         | >= 1.12.11        |
+-----------------------------+---------------+-------------------+-------------------+
| CUDA (GPU image only)       | 9.0           | 9.0               | 10.1              |
+-----------------------------+---------------+-------------------+-------------------+
| numpy                       | >=1.14.3      | >=1.15.2          | 1.16.4            |
+-----------------------------+---------------+-------------------+-------------------+
| Pillow                      | >=5.1.0       | >=5.2.0           | 6.0.0             |
+-----------------------------+---------------+-------------------+-------------------+
| pip                         | >=10.0.1      | >=18.0            | >=18.0            |
+-----------------------------+---------------+-------------------+-------------------+
| python-dateutil             | >=2.7.3       | >=2.7.3           | >=2.7.3           |
+-----------------------------+---------------+-------------------+-------------------+
| retrying                    | >=1.3.3       | >=1.3.3           | 1.3.3             |
+-----------------------------+---------------+-------------------+-------------------+
| s3transfer                  | >=0.1.13      | >=0.1.13          | >=0.1.13          |
+-----------------------------+---------------+-------------------+-------------------+
| sagemaker-containers        | >=2.1.0       | >=2.1.0           | 2.4.10.post0      |
+-----------------------------+---------------+-------------------+-------------------+
| sagemaker-pytorch-container | 1.0           | 1.1               | 1.2               |
+-----------------------------+---------------+-------------------+-------------------+
| setuptools                  | >=39.2.0      | >=40.4.3          | >=40.4.3          |
+-----------------------------+---------------+-------------------+-------------------+
| six                         | >=1.11.0      | >=1.11.0          | 1.12.0            |
+-----------------------------+---------------+-------------------+-------------------+
| torch                       | 0.4.0         | 1.0.0             | 1.1.0             |
+-----------------------------+---------------+-------------------+-------------------+
| torchvision                 | 0.2.1         | 0.2.1             | 0.3.0             |
+-----------------------------+---------------+-------------------+-------------------+
| Python                      | 2.7 or 3.5    | 2.7 or 3.6        | 2.7 or 3.6        |
+-----------------------------+---------------+-------------------+-------------------+

The Docker images extend Ubuntu 16.04.

If you need to install other dependencies you can put them into `requirements.txt` file and put it in the source directory
(``source_dir``) you provide to the `PyTorch Estimator <#pytorch-estimators>`__.

You can select version of PyTorch by passing a ``framework_version`` keyword arg to the PyTorch Estimator constructor.
Currently supported versions are listed in the above table. You can also set ``framework_version`` to only specify major and
minor version, which will cause your training script to be run on the latest supported patch version of that minor
version.

Alternatively, you can build your own image by following the instructions in the SageMaker Chainer containers
repository, and passing ``image_name`` to the Chainer Estimator constructor.

You can visit `the SageMaker PyTorch containers repository <https://github.com/aws/sagemaker-pytorch-containers>`_.
