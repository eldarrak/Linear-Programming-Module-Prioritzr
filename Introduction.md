

<div id="top"></div>


<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/CageCode/Linear-Programming-Module-Prioritzr">
    <img src="images/LP_in_R.jpg" alt="Logo" width="600" height="480">
  </a>

  <h3 align="center">Linear Programming in R using PrioritizR package and examples</h3>

  <p align="center">
    By: Daniël Kooij
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#LP in R">Why linear programming in R?</a>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#Gurobi">Gurobi</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
  </ol>
</details>



<!-- LP in R -->
## Why linear programming in R?

Earlier this week you have learned what linear programming is all about. You have seen examples of some problems where an optimal solution can be found, such as for the two-crops example. Finding the solution to a linear programming problem with limited amount of dimensions and constraints can be done even by hand. However, when the number of dimensions and constraints keep increasing it becomes almost impossible to calculate the optimal solution(s). Moreover, the problem might even exceed the amount of computing power that is reasonably available to calculate all possible solutions to the problem. In that case, we need some sort of algorithm to scan the problem space in order to find an optimal solution. This is why we will use R in this module, to make use of algorithms that can solve linear programming problems for us. 

One of the fields were linear programming problems occur is in the field of conservation ecology. Imagine you are tasked by indicating which areas of a forest should be protected in order to preserve the maximum amount of biodiversity in this park. You open your prefered GIS software and import different kinds of maps to base your decision on. The imported maps show the occurence and observations of tens of different type of species, the spatial availability of various nutrients, soil maps, hydrological maps, land covers, and so forth... Where do you even start to determine the areas that are most important to preserve?
This is were linear programming in a statistical software comes in: By defining the objectives and constraints, a solution can be found using R. In this module we will look at spatial linear programming problems and solve those using a package specifically designed for conservation planning problems named: **PrioritizR**. The designers of the Prioritizr package summarize its functionality as follows:

* _The prioritizr R package uses integer linear programming (ILP) techniques to provide a flexible interface for building and solving conservation planning problems. It supports a broad range of objectives, constraints, and penalties that can be used to custom-tailor conservation planning problems to the specific needs of a conservation planning exercise. Once built, conservation planning problems can be solved using a variety of commercial and open-source exact algorithm solvers. In contrast to the algorithms conventionally used to solve conservation problems, such as heuristics or simulated annealing, the exact algorithms used here are guaranteed to find optimal solutions. Furthermore, conservation problems can be constructed to optimize the spatial allocation of different management actions or zones, meaning that conservation practitioners can identify solutions that benefit multiple stakeholders._

Sounds like quite the package! Let's see how it works and what we can do with it. Before we can start, we first need to install the **PrioritizR** package in R and also a software package called **Gurobi** that applies algorithms to efficiently solve the linear programming problems at hand.

<br />
<div align="center">
  <img src="images/Protected_areas_Madagascar.PNG" alt="Logo" width="600" height="480">
  <br />
  <em>Fig 1. Typical conservation planning problem, where protected areas are indicated in pink</em>
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
* Open command prompt (Windows users can use the search function on laptop) and type: _grbgetkey [your-key]_, where your-key is the key you found in the previous step.
* If all previous steps are completed, you succesfully installed the Gurobi software.

If you are not able to succesfully install the software, then a more elaborate installation guide can be found here:
* ([https://prioritizr.net/articles/gurobi_installation.html](https://prioritizr.net/articles/gurobi_installation_guide.html))

<br />

### Installation

Once the software is installed on your laptop, the Gurobi package can be installed in Rstudio. Use the following code to install the latest version of the Gurobi software which is 10.0.0. to this date (**10/12/22**). You are probably prompted to also install dependencies like the package _slam_ in order to make the Gurobi package work, also install this package with the provided code.


```R
# Install Gurobi1000
install.packages("c:/gurobi100/win64/R/gurobi_10.0-0.zip", repos = NULL)

# Install additionals
install.packages("slam", repos = "https://cloud.r-project.org")
```

If the packages are installed correctly, you can continue, if not; ask the teacher for assistance. 


<p align="center">(<a href="https://github.com/eldarrak/Linear-Programming-Module-Prioritzr/blob/main/PrioritzR_Assignment.md">Continue with Prioritizr</a>)</p>






