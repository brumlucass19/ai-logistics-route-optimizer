# RotaSmart

Final project for the Building AI course

## Summary

RotaSmart is an AI tool that helps small and mid-sized logistics operators plan delivery routes that minimize distance, fuel costs, and delivery time, while respecting real-world constraints like vehicle capacity and delivery time windows. Building AI course project.

## Background

Route planning is one of the most common and costly problems in logistics and operations. Even a small delivery fleet can face millions of possible route combinations once you factor in multiple stops, vehicle capacity, and time windows — a classic combinatorial explosion, similar to the Traveling Salesperson Problem covered in this course.

Why this matters to me:
* I have over 10 years of experience in operations, logistics, and process management, and I've seen firsthand how manually planned routes waste fuel, driver hours, and money.
* Many small and mid-sized logistics companies in Brazil still plan routes manually or with very basic tools, unlike large players who already use sophisticated optimization software.
* Small inefficiencies compound: a 10% reduction in route distance across hundreds of deliveries per day adds up to real savings in fuel, driver overtime, and carbon emissions.

This is a problem I've personally encountered in previous logistics roles, where route planning was done largely by experience and intuition rather than data — leaving a lot of room for improvement.

## How is it used?

RotaSmart would be used by:
* **Dispatchers and logistics coordinators** at small/mid-sized delivery companies, who currently plan routes manually or with spreadsheets
* **Independent delivery fleet owners** who don't have access to expensive enterprise route optimization software

**Typical use case:** At the start of the day (or the night before), the dispatcher inputs the day's delivery addresses, each vehicle's capacity, and any delivery time windows. RotaSmart returns an optimized route assignment for each vehicle, minimizing total distance/time while respecting constraints. The dispatcher can review and manually adjust the suggested routes before sending them to drivers.

**Who is affected:**
* Drivers, who benefit from shorter, less stressful routes
* Customers, who benefit from more reliable delivery time estimates
* The company, which saves on fuel and labor costs
* The environment, through reduced fuel consumption and emissions

## Data sources and AI methods

**Data needed:**
* Delivery addresses (converted to coordinates via a geocoding API)
* Distance/travel time between points (via a mapping API such as [OpenStreetMap](https://www.openstreetmap.org/) or Google Maps Distance Matrix API)
* Vehicle capacity and number of available vehicles
* Delivery time windows (if applicable)
* Historical delivery data (actual vs. planned times), if available, to improve future estimates

**AI/optimization techniques:**
* The core problem is a variant of the **Traveling Salesperson Problem (TSP)** / **Vehicle Routing Problem (VRP)**, both covered in this course under search and optimization.
* For small numbers of stops, a **brute-force** approach (enumerating all routes) can find the exact optimal solution, just like in the pineapple-shipping example from this course.
* For realistic numbers of stops (where brute force becomes infeasible due to combinatorial explosion), **hill climbing** and **simulated annealing** — both covered in this course — can be used to find a good (though not necessarily perfect) solution in reasonable time.
* If historical delivery data becomes available, a simple **linear regression** model could help predict more realistic travel times between points (accounting for traffic patterns, time of day, etc.), rather than relying on straight-line or default map distances.

A simple demo implementation could:
1. Take a small list of delivery addresses (5–10 stops) as input
2. Build a distance matrix, similar to the pineapple shipping exercise in this course
3. Use simulated annealing to find a low-cost route
4. Output the suggested route order and estimated total distance/time

## Challenges

RotaSmart does not solve everything:
* It doesn't account for real-time traffic conditions or unexpected road closures unless integrated with a live traffic API (which adds cost and complexity)
* It relies on the accuracy of address geocoding — bad or incomplete addresses will lead to bad route suggestions
* It doesn't replace a dispatcher's judgment: local knowledge (a driver knows a shortcut, a customer prefers a specific delivery time) may not be captured in the model
* Ethically, over-optimizing routes purely for cost could lead to excessive pressure on drivers (unrealistic time expectations); any deployment should keep realistic buffers and driver wellbeing in mind
* Like any optimization approach based on heuristics (hill climbing/simulated annealing), the solution found is not guaranteed to be the mathematically optimal one, only a good approximation

## What next?

* Add a simple web interface so dispatchers without coding experience can input addresses and get routes without touching code
* Integrate a real mapping API for accurate travel times instead of straight-line distances
* Incorporate real-time traffic data for more accurate route timing
* Extend the model to handle multiple vehicles simultaneously (full Vehicle Routing Problem) rather than a single route
* Partner with a small logistics company to pilot the tool with real delivery data and measure actual fuel/time savings

To move forward, I'd need: stronger Python skills (currently building this through self-study), access to a mapping/geocoding API, and ideally a logistics company willing to pilot test the tool with real data.

## Acknowledgments

* Route optimization concepts (state space, transitions, brute force, hill climbing, simulated annealing) as taught in the [Building AI](https://buildingai.elementsofai.com/) and [Elements of AI](https://www.elementsofai.com/) courses by Reaktor and the University of Helsinki
* Inspiration from the Traveling Salesperson Problem, a classic problem in computer science and operations research

