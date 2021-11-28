
<div id="top"></div>


<!-- PROJECT LOGO -->
<br />
<div align="center">
  <img src="images/logo_prioritizr.png" alt="Logo" width="240" height="300">
  </a>

  <h3 align="center">Using the PrioritizR Package</h3>

  <p align="center">
    By: Daniël Kooij
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#PPP">Preparing your first PriotizR Project</a>
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
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- PPP -->
## Preparing your first PriotizR Project

In this section, we are going to explore step by step how linear programming can be implemented on a spatial scale. For this purpose, we will imagine the aforementioned task; indicating which areas of a forest should be protected in order to preserve .....the maximum amount of biodiversity? Suppose the forest in question is a perfect square of 10 by 10 kilometers, divided into grid cells of 1 km^2. Each grid cell of forest may attain the _preserved_ status, but there can only be a limited amount of grid cells that can be preserved due to some constraint(s).

Question 1. What might be a limiting factor for preservation? I.e. What could be a reason that we cannot preserve the whole forest?

Answer 1. There can be many limiting factors. Often there is money involved and the conservation costs are too high. However, there may be other reasons, such as: The entire forest cannot be managed and patrolled, or preservation could mean the preserved area would be fenced off and the government decided that at least _X_% of the forest should be remain open to the public. 


Question 2. What kind of data (variables) would you like to know about each grid cell of forest to determine if it should be preserved or not? Name three different types of variables.



- Explain input features and data




```R
# load packages
library(prioritizr)
library(gurobi)
```


We will use the sim_pu_polygons object to represent our planning units. Although the prioritizr R can support many different types of planning unit data, here our planning units are represented as polygons in a spatial vector format (i.e. SpatialPolygonsDataFrame). Each polygon represents a different planning unit and we have 90 planning units in total. The attribute table associated with this dataset contains information describing the acquisition cost of each planning (“cost” column), and a value indicating if the unit is already located in protected area (“locked_in” column). Let’s explore the planning unit data.


Earlier this week you have learned what linear programming is all about. You have seen examples of some problems where an optimal solution can be found (INSERT EXAMPLE WHAT THEY DID). Finding the solution to a linear programming problem with limited amount of dimensions and constraints can be done even by hand (as you have seen this week??). However, when the number of dimensions and constraints keep increasing it becomes almost impossible to calculate the optimal solution(s). Moreover, the problem might even exceed the amount of computing power that is reasonably available to calculate all possible solutions to the problem. In that case, we need some sort of algorithm to scan the problem space in order to find an optimal solution. This is why we will use R in this module, to make use of algorithms that can solve linear programming problems for us. 

One of the fields were linear programming problems occur is in the field of conservation ecology. Imagine you are tasked by indicating which areas of a forest should be protected in order to preserve the maximum amount of biodiversity in this park. You open your prefered GIS software and import different kinds of maps to base your decision on. The imported maps show the occurence and observations of tens of different type of species, the spatial availability of various nutrients, soil maps, hydrological maps, land covers, and so forth... Where do you even start to determine the areas that are most important to preserve?
This is were linear programming in a statistical software comes in: By defining the objectives and constraints, a solution can be found using R. In this module we will look at spatial linear programming problems and solve those using a package specifically designed for conservation planning problems named: **PrioritizR**. Before we can start, we first need to install the **PrioritizR** package in R and also a software package called **Gurobi** that applies algorithms to efficiently solve the linear programming problems at hand.

<br />
<div align="center">
  <img src="images/Protected_areas_Madagascar.PNG" alt="Logo" width="600" height="480">
  <br />
  <em>Typical conservation planning problem, where protected areas are indicated in pink</em>
</div>

<br />


<!-- GETTING STARTED -->
## Getting Started

The latest official version of the prioritizr R package can be installed from the Comprehensive R Archive Network (CRAN) using the following R code. Copy the code and run it in Rstudio, make sure your R version is 4.+ (you probably already checked this previous week).

```R
# Install the prioritizr package
install.packages("prioritizr", repos = "https://cran.rstudio.com/")
```

### Gurobi

Next, we will need to install a so-called solver, which is software that uses algorithms to solve linear programming problems quickly. [Gurobi](https://www.gurobi.com/) is an example of such type of software, which we are going to install and use in this module. Gurobi is not open-source software, but academic users may register for a one-year free trial. In short, we will perform the following steps to install this software:

* Register for a free academic trial [Here](https://pages.gurobi.com/registration).
* Change your password with the email you receive.
* Login to the Gurobi website.
* Download the software: (https://www.gurobi.com/downloads/gurobi-software/)
* Go to (https://www.gurobi.com/downloads/free-academic-license/) and find your key under Installation.
* Open command prompt (Windows users can use the search function on laptop) and type: grbgetkey [your-key], where your-key is the key you found in the previous step.
* If all previous steps are completed, you succesfully installed the Gurobi software.

If you are not able to succesfully install the software, then a more elaborate installation guide can be found here:
* (https://prioritizr.net/articles/gurobi_installation.html)


### Installation

Once the software is installed on your laptop, the Gurobi package can be installed in Rstudio. Use the following code to install the latest version of the Gurobi software which is 9.5.0. to this date (**19/11/21**). You are probably prompted to also install dependencies like the package _slam_ in order to make the Gurobi package work, also install this package with the provided code.


```R
# Install Gurobi950
install.packages("c:/gurobi950/win64/R/gurobi_9.5-0.zip", repos = NULL)

# Install additionals
install.packages("slam", repos = "https://cloud.r-project.org")
```

If the packages are installed correctly, you can continue, if not; ask the teacher for assistance. 


<p align="center">(<a href="#top">back to top</a>)</p>













_Below is an example of how you can instruct your audience on installing and setting up your app. This template doesn't rely on any external dependencies or services._


3. Install NPM packages
   ```sh
   npm install
   ```
4. Enter your API in `config.js`
   ```js
   const API_KEY = 'ENTER YOUR API';
   ```

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage

Use this space to show useful examples of how a project can be used. Additional screenshots, code examples and demos work well in this space. You may also link to more resources.

_For more examples, please refer to the [Documentation](https://example.com)_

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- ROADMAP -->
## Roadmap

- [x] Add Changelog
- [x] Add back to top links
- [ ] Add Additional Templates w/ Examples
- [ ] Add "components" document to easily copy & paste sections of the readme
- [ ] Multi-language Support
    - [ ] Chinese
    - [ ] Spanish

See the [open issues](https://github.com/othneildrew/Best-README-Template/issues) for a full list of proposed features (and known issues).

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- CONTACT -->
## Contact

Your Name - [@your_twitter](https://twitter.com/your_username) - email@example.com

Project Link: [https://github.com/your_username/repo_name](https://github.com/your_username/repo_name)

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

Use this space to list resources you find helpful and would like to give credit to. I've included a few of my favorites to kick things off!

* [Choose an Open Source License](https://choosealicense.com)
* [GitHub Emoji Cheat Sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet)
* [Malven's Flexbox Cheatsheet](https://flexbox.malven.co/)
* [Malven's Grid Cheatsheet](https://grid.malven.co/)
* [Img Shields](https://shields.io)
* [GitHub Pages](https://pages.github.com)
* [Font Awesome](https://fontawesome.com)
* [React Icons](https://react-icons.github.io/react-icons/search)

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/othneildrew/Best-README-Template.svg?style=for-the-badge
[contributors-url]: https://github.com/othneildrew/Best-README-Template/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/othneildrew/Best-README-Template.svg?style=for-the-badge
[forks-url]: https://github.com/othneildrew/Best-README-Template/network/members
[stars-shield]: https://img.shields.io/github/stars/othneildrew/Best-README-Template.svg?style=for-the-badge
[stars-url]: https://github.com/othneildrew/Best-README-Template/stargazers
[issues-shield]: https://img.shields.io/github/issues/othneildrew/Best-README-Template.svg?style=for-the-badge
[issues-url]: https://github.com/othneildrew/Best-README-Template/issues
[license-shield]: https://img.shields.io/github/license/othneildrew/Best-README-Template.svg?style=for-the-badge
[license-url]: https://github.com/othneildrew/Best-README-Template/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/othneildrew
[product-screenshot]: images/screenshot.png
