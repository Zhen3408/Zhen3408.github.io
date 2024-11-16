---
name: HW6 Visualization Project
tools: [Python, HTML, vega-lite]
image: assets/pngs/cars.png
description: This is a "showcase" project that uses vega-lite for interactive viz!
custom_js:
  - vega.min
  - vega-lite.min
  - vega-embed.min
  - justcharts
---


# HW6 Visualization

## Total Square Footage by City per Agency

### Select an Agency
<select id="agency-select">
    <option value="building_count_by_city_for_Department_of_Natural_Resources.json">Department of Natural Resources</option>
    <option value="building_count_by_city_for_Department_of_Corrections.json">Department of Corrections</option>
    <option value="building_count_by_city_for_Department_of_Human_Services.json">Department of Human Services</option>
    <option value="building_count_by_city_for_Department_of_Transportation.json">Department of Transportation</option>
    <option value="building_count_by_city_for_Department_of_State_Police.json">Department of State Police</option>
    <option value="building_count_by_city_for_Department_of_Military_Affairs.json">Department of Military Affairs</option>
    <option value="building_count_by_city_for_Department_of_Agriculture.json">Department of Agriculture</option>
    <option value="building_count_by_city_for_Governors_State_University.json">Governors State University</option>
    <option value="building_count_by_city_for_Department_of_Central_Management_Services.json">Department of Central Management Services</option>
    <option value="building_count_by_city_for_Illinois_State_University.json">Illinois State University</option>
    <option value="building_count_by_city_for_Historic_Preservation_Agency.json">Historic Preservation Agency</option>
    <option value="building_count_by_city_for_Department_of_Juvenile_Justice.json">Department of Juvenile Justice</option>
    <option value="building_count_by_city_for_Southern_Illinois_University.json">Southern Illinois University</option>
    <option value="building_count_by_city_for_Illinois_Medical_District_Commission.json">Illinois Medical District Commission</option>
    <option value="building_count_by_city_for_University_of_Illinois.json" selected>University of Illinois</option>
    <option value="building_count_by_city_for_Department_of_Veterans__Affairs.json">Department of Veterans' Affairs</option>
    <option value="building_count_by_city_for_Chicago_State_University.json">Chicago State University</option>
    <option value="building_count_by_city_for_Northern_Illinois_University.json">Northern Illinois University</option>
    <option value="building_count_by_city_for_Office_of_the_Secretary_of_State.json">Office of the Secretary of State</option>
    <option value="building_count_by_city_for_Illinois_Emergency_Management_Agency.json">Illinois Emergency Management Agency</option>
    <option value="building_count_by_city_for_Western_Illinois_University.json">Western Illinois University</option>
    <option value="building_count_by_city_for_Eastern_Illinois_University.json">Eastern Illinois University</option>
    <option value="building_count_by_city_for_Northeastern_Illinois_University.json">Northeastern Illinois University</option>
    <option value="building_count_by_city_for_Illinois_Community_College_Board.json">Illinois Community College Board</option>
    <option value="building_count_by_city_for_Illinois_Board_of_Higher_Education.json">Illinois Board of Higher Education</option>
    <option value="building_count_by_city_for_IL_State_Board_of_Education.json">IL State Board of Education</option>
    <option value="building_count_by_city_for_Department_of_Revenue.json">Department of Revenue</option>
    <option value="building_count_by_city_for_Governor_s_Office.json">Governor's Office</option>
    <option value="building_count_by_city_for_Office_of_the_Attorney_General.json">Office of the Attorney General</option>
    <option value="building_count_by_city_for_Appellate_Court___Fourth_District.json">Appellate Court / Fourth District</option>
    <option value="building_count_by_city_for_Department_of_Public_Health.json">Department of Public Health</option>
    <option value="building_count_by_city_for_Illinois_Courts.json">Illinois Courts</option>
    <option value="building_count_by_city_for_Appellate_Court___Third_District.json">Appellate Court / Third District</option>
    <option value="building_count_by_city_for_Appellate_Court___Fifth_District.json">Appellate Court / Fifth District</option>
    <option value="building_count_by_city_for_Appellate_Court___Second_District.json">Appellate Court / Second District</option>
</select>

<div id="chart-container" style="width: 100%; margin-top: 20px;"></div>

<script>
  // Load a default chart on page load
  document.addEventListener('DOMContentLoaded', () => {
    const defaultFile = "building_count_by_city_for_University_of_Illinois.json"; // Default JSON file
    document.getElementById('agency-select').value = defaultFile; // Set dropdown value
    loadChart(defaultFile); // Load default chart
  });

  // Function to load and display a chart
  function loadChart(agencyJson) {
    const chartDiv = document.getElementById('chart-container');
    chartDiv.innerHTML = ''; // Clear the previous chart
    if (agencyJson) {
      vegaEmbed('#chart-container', `{{ site.baseurl }}/assets/json/${agencyJson}`).catch(console.error);
    }
  }

  // Dropdown selection handler
  const dropdown = document.getElementById('agency-select');
  dropdown.addEventListener('change', (event) => {
    const selectedFile = event.target.value;
    loadChart(selectedFile);
  });

</script>

## Building Square Footage Over Time(Since 1950)
<vegachart schema-url="{{ site.baseurl }}/assets/json/building_scatter.json" style="width: 100%"></vegachart>

## Write-Up for Visualization 1: Total Square Footage by City per Agency

**Description**  
The first visualization is a bar chart that shows the total square footage of buildings for each agency. 
The primary goal is to provide a clear comparison of the total building footprint among different agencies, 
helping users understand which agencies have the largest or smallest building areas. Each agency is represented by 
a distinct color for easy differentiation.

**Encoding Types**:  
  - The x-axis encodes `Agency Name` as a nominal categorical variable.  
  - The y-axis encodes the `Square Footage` as a quantitative variable, displaying the total building area for each agency.  
  - The bars are colored using a categorical color scheme to make each agency visually distinct.  
**Color Scheme**: A `Category10` color scheme was chosen to provide high contrast between categories, making it easier for users to distinguish between agencies.  

**Data Transformations**  
In the data preparation phase, the dataset was grouped by `Agency Name`, and the total square footage was aggregated. This allowed us to focus on the cumulative data for each agency rather than showing individual building entries. 

**Interactivity**
A dropdown selection box was added in to let user choose which agency to look at. The json file of each agency was generated and saved under the  `asset` directory. A javascript event listener was added to handle the switch of loading different chart.
---

## Write-Up for Visualization 2: Building Square Footage Over Time

**Description**  
The second visualization is a scatter plot that illustrates the total square footage of buildings constructed by 
year and grouped by agency. Each point represents a specific year and the total square footage of buildings 
constructed by an agency in that year. The visualization aims to identify trends, such as peaks in construction 
activity for certain agencies or time periods.

**Encoding Types**:  
  - The x-axis encodes `Year Constructed` as an ordinal variable, with each year represented as a discrete point.  
  - The y-axis encodes `Square Footage` as a quantitative variable, showing the total building area constructed in each year.  
  - The color encodes `Agency Grouped` to allow easy differentiation between agencies.  
  - The size of the points encodes the `Square Footage` again, providing an additional layer of insight into how much space was added in each year.  
**Color Scheme**: Each angency has a different color, ensuring distinct visual separation.  


**Data Transformations**  
Data was filtered to include only the years from 1950 to 2020 to reduce noise and focus on relevant periods.

## Write-Up about Homework 5
I am doing the similar plots to my Homework5. The basic data filtering and altair chart encoding is similar to my previous
work. The main differences is to achieve the interactivity. As I mentioned above, an HTML style select box was added and javascript
event listener was added to ensure different charts are loaded when selecting different agency. Compared with homework 5, this time
my work is kind of more dirty (or low memory efficiency) because I have to save each single json file of different agencies.

## Search The Data & Methods

Below is where we can put some links to both the data and the analysis code as buttons:

<!-- these are written in a combo of html and liquid --> 

<div class="left">
{% include elements/button.html link="https://github.com/Zhen3408/Zhen3408.github.io/tree/main/assets/json" text="The Data" %}
</div>

<div class="right">
{% include elements/button.html link="https://github.com/Zhen3408/Zhen3408.github.io/blob/main/python_notebooks/hw6_notebook.ipynb" text="The Analysis" %}
</div>

