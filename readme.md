<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [Notes on gitlab-ci-pipelines-ci-cd-and-devops-for-beginners on udemy](#notes-on-gitlab-ci-pipelines-ci-cd-and-devops-for-beginners-on-udemy)
  - [Intro](#intro)
    - [Your first pipeline](#your-first-pipeline)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Notes on gitlab-ci-pipelines-ci-cd-and-devops-for-beginners on udemy

## Intro

### Your first pipeline

Build -> Test

- Create gitlab project
- click on "Set up CI/CD" or create a `.gitlab-ci.yml` file in the base of the project manually

Example:

        # name of job (task:)
        build the car:
          script:
            # shell commands 
            - mkdir build
            - cd build
            - touch car.txt
            - echo "chassis" > car.txt
            - echo "engine" >> car.txt
            - echo "wheels" >> car.txt

Commit the file and gitlab will detect the pipeline. An indicator (running, passed, failed) will be visible in the main project view on the upper right:

![pipeline indicator](readme_images/gitlab_pipleline_progress.png)

Clicking on the indicator and then on the job ("build the car") in the lower half - a pipeline can contain multiple jobs - the pipeline's output is displayed:

![pipeline indicator](readme_images/gitlab_pipleline_output.png)

We can specify multiple jobs, so we'll add a test job:

build the car:
    script:
    # shell commands 
        - mkdir build
        - cd build
        - touch car.txt
        - echo "chassis" > car.txt
        - echo "engine" >> car.txt
        - echo "wheels" >> car.txt

test the car:
    script:
        # test if file exists
        # it will fail the pipeline if it doesn't
        - test -f build/car.txt
        - cd build
        - grep "chassis" car.txt
        - grep "engine" car.txt
        - grep "wheels" car.txt
