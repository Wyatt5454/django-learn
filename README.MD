<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->

<a name="readme-top"></a>

<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Don't forget to give the project a star!
*** Thanks again! Now go create something AMAZING! :D
-->

<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/github_username/repo_name">
    <img src="photo.jpg" alt="Logo" width="80" height="80">
  </a>

<h3 align="center">project_title</h3>

  <p align="center">
    project_description
    <br />
    <a href="https://github.com/github_username/repo_name"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/github_username/repo_name">View Demo</a>
    ·
    <a href="https://github.com/github_username/repo_name/issues">Report Bug</a>
    ·
    <a href="https://github.com/github_username/repo_name/issues">Request Feature</a>
  </p>
</div>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <ul><li><a href="#docker-explained" >Docker Explained </a></li></ul>
    <li><a href="#contributing">Contributing</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->

## About The Project

[![Product Name Screen Shot][product-screenshot]](https://example.com)

Wyatts Djano app to learn on

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Built With

- [![Django][Django]][https://www.djangoproject.com/]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- GETTING STARTED -->

## Getting Started

Instructions on how to start local development and run from a container

### Prerequisites

This is an example of how to list things you need to use the software and how to install them.
** python3
** pip

### Installation

1. Install django and dependencies through pip
2. Clone the repo
   ```sh
   git clone git@github.com:Wyatt5454/django-learn.git
   ```
3. Install python packages
   ```sh
   pip install django django-debug-toolbar
   ```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- USAGE EXAMPLES -->

## Usage

### Running local dev server

1. Naviage to the root dir after installation
2. ```sh
   python manage.py runserver
   ```

### Running as docker container

1. Build the source image first
2. ```sh
   docker build . -t django_image
   ```
3. Run the image, naming the container and exposing the port we want to the UI
4. ```sh
   docker run -d --name django_container -p 8000:8000 django_image
   ```
5. The UI should be available at 127.0.0.1:8000 though it is a dev server

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Docker explained

When we create a docker container, we are doing our best to emulate the deployment environment by creating a source container that runs in all environment. We are using docker here, but a common alternative for Linux is Podman. It is identical, Docker can be aliased to Podman and vice versa.
So how does this work?
First we run the build script. 
```sh
   docker build . -t django_image
```
This script tells docker to build a container using the Dockerfile in the root dir, ., and to tag the image as "django_image".
If no dockerfile in the root dir, we have to specify the file with `docker build -f filename -t django_image`

Once we have the image built, we must run the image in a container. The image is the application, while the container is the virutal environment that is agnostic of hardware and can be deployed anywhere. 
```sh
   docker run -d --name django_container -p 8000:8000 django_image
```
1. This script tells docker to run in a detached head (-d), so it does not take over our terminal. 
2. It names the container (--name) so it is easier to access. If we do not name the container, a random name is generated (name like whizzy_cheese or flying_eflutter, very random). 
3. The script also tells the container to expose port 8000 and to map the containers external port 8000 to the images internal port 8000 (-p 8000:8000). This is slightly more complicate, but basically the web app runs inside the container, and only exposes network traffic INTERNAL to the container. You can see we define this internal traffic by defining the variable `EXPOSE 8000` in the Dockerfile. Now that is all fine, but we also need the traffic to be exposed OUTSIDe of the container as well to actually see the work we are doing in whatever browser we are using to hit `127.0.0.1:8000`. To do this, we define the port mapping, and map the internal port of 8000 to the external port of 8000 (-p 8000[internal]: 8000[external]). The internal and external ports are almost always mapped to the same port number in my personal experience.
4. Lastly the script denotes the image we want to run in the container, and we use the tag name `django_image`. 
5. All of this results in a container running on your local machine acting as a dev server. 

Quick note, this IS NOT MEANT TO REPLACE THE ACTIVE DEV SERVER WE RUN WITHOUT CONTAINERS. While running containers on our local machine is nice, this is 99% used to validate deployment, or keep a linux OS running we may need. This is significantly slower than developing in a local env, as it takes ~2 minutes to spin up a container from scrach, while running a dev server takes ~2 seconds. When spinning up a new container, MAKE SURE TO DELETE THE SOURCE IMAGE or it will be used next time you run the container.

<!-- CONTRIBUTING -->

## Contributing

Steps to contribute to the project

1. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
2. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
3. Push to the Branch (`git push origin feature/AmazingFeature`)
4. Open a Pull Request

<p align="right">(<a href="#readme-top">back to top</a>)</p>
