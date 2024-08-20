# Distributed Training on A3-Mega (H100x8) with Vertex
This repo provides examples on how to launch distributed training on A3-Mega (H100x8) on Vertex

This repo contains:

## 1.1 - Pretraining Llama2-7B with Nemo (Pytorch)
Follow these steps to run this example:

- **Dockerfile**: using the provided [Dockerfile](nemo/llama2-7b/Dockerfile), build an image from [NVIDIA Nemo image](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/nemo/tags).
- **Nemo Config**: Use the [llama2-7b.yaml](nemo/llama2-7b/llama2-7b.yaml) Nemo config file as the reference - you can either use it as is or modify it to your liking.
- **Entry script**: The [job.sh](nemo/llama2-7b/job.sh) bash script contains the script to set the required environment variabls for `TCPXO` and the `torchrun` launcher to start the Nemo pretraining job.
- **Vertex payload**: The [vertex-payload.json](nemo/llama2-7b/vertex-payload.json) file to start a job in Vertex. Make sure you set the right value for the `NNODES` environment variable to reflect the right number of nodes participating in your training job.
- **Submit the job**: Use the following curl command to kick off the job on Vertex:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @nemo/llama2-7b/vertex-payload.json \
     "https://<reigon>-aiplatform.googleapis.com/v1/projects/<project-id>/locations/<reigon>/customJobs"
```
## 1.2 - Pretraining Llama3-70B with Nemo (Pytorch)
The same steps as 1.1 apply (except please refer to nemo/llama3-70b directory). Use the following command to kick off the job:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @nemo/llama3-70b/vertex-payload.json \
     "https://<reigon>-aiplatform.googleapis.com/v1/projects/<project-id>/locations/<reigon>/customJobs"
```

## 2- Stable Diffusion Diffusers with WebDataset (Pytorch)
*Coming soon*

## 3- Pretraining Llama2-7B with MaxText (JAX)
*Coming soon*

