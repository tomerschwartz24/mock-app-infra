# mock-app application helm infra chart

## This repo contain the application custom helm chart 

- The CI pipeline make sure to update the application values.yaml (image.tag) file with the appropriate tag in runtime based on the $BUILD_NUMBER of the pipeline

# Architecture 


  <img src="mock-app-arch.png" alt="alt text" width="800" height="600"> <br>