---
author: "Minh T. Nguyen"
title: "S.O.L.I.D Principles Explained"
date: "2023-04-28"
description: "Robert C. Martin (Uncle Bob)'s S.O.L.I.D principles in software engineering explained with Python examples through the lense of web development and machine learning applications."
tags: ["solid principles", "python", "web development", "data science", "long-read"]
categories: ["software engineering", "machine-learning"]
series: ["Software Engineering"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: false
weight: 5
---
<p style="color: #286EE0"><strong>Status:</strong> [Latest]</p>

I recently finished an excellent graduate course, Software Engineering (CS5704), and learned about different aspects of software projects and how different-size companies handle their technical/business changes to deliver successful products to their customer. Some important topics are Process Models (Waterfall, V-Model, Spiral, Agile), Requirements Definition, and Architecture Design Patterns. Especially, S.O.L.I.D principles have struck me as must-known concepts for writing better and cleaner code.

**Why do S.O.L.I.D principles matter?**
According to Uncle Bob, bad code slows down the development team as it is **confusing** and **fragile**. Confusing code does not explain what it is doing, while fragile code breaks in many places when you change one or a few lines of code.


What we want is the code that is **clear**, **rigid**, and **reusable**.

***Fun Fact:** In his talk in S.O.L.I.D Principles, he mentioned that he was not the first to realize or coin the acronym "SOLID.”*

## <span style="color:#286EE0">S</span>ingle Responsibility Principle

**SRP**: *"A class should have one, and only one reason to change"* — Robert C. Martin. In Object Oriented Programming (OOP), a class should have only one primary function. If there is more than one utility for that class, we should split it into multiple courses. This helps distribute the functional responsibilities across numerous classes or objects (or developers).

<center>
    <img style="width: 50%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/solid_principles/imgs/cartoons/code_blame_cartoon.png" />
</center>
<figcaption class="img_footer">
    Fig. 1. Don't let your code (or yourself) take on all the responsibilties in the project. Divide and conquer! (Image source: 
    <a href="https://www.monkeyuser.com/2018/blame/" class="img_footer">MonkeyUser.com</a>).
</figcaption>

### Web Development Example
Let's say you are a developer in the Google Shopping team who is in charge of designing a class to process post-item-purchase.

<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class PostPurchaseProcess:
    def web_notification(self, message):
        """
        Code to send confirmation bill to Google Chrome
        """
        pass
    
    def email_notification(self, message):
        """
        Code to send confirmation bill to Gmail
        """
        pass
    
    def phone_notification(self, message):
        """
        Code to send confirmation bill to Google Pixel
        """
        pass
```
</p></details>
</br>

In the example above, the class `PostPurchaseProcess` violates the SRP as it contains too many responsibilities: sending notifications to web app, email, and mobile. What if there are errors in sending notifications to Google Pixel and Gmail? It may take time to pinpoint precisely which function(s) is responsible for the mistake!

**Fix:** We can refactor the code into multiple classes, each with single responsibility.

<center>
    <img style="width: 70%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/solid_principles/imgs/diagrams/srp.png" />
</center>
<figcaption class="img_footer">
    Fig. 2. Design refactored with single responsibility principle.
</figcaption>

</br>

<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class WebPurchaseProcess:
    def web_notification(self, message):
        """
        Code to send confirmation bill to Google Chrome
        """
        pass

class EmailPurchaseProcess:
    def email_notification(self, message):
        """
        Code to send confirmation bill to Gmail
        """
        pass

class PhonePurchaseProcess:
    def phone_notification(self, message):
        """
        Code to send confirmation bill to Google Pixel
        """
        pass
```
</p></details>
</br>

### Data Science Example
Suppose you are a Data Scientist at C3.ai who is processing a tabular dataset for a supervised classification application. There are multiple steps to investigate the structure, quality, and content of the dataset, such as: checking datatypes, removing duplicates, data imputation, removing outliers, class-balancing, feature analysis, or feature engineering. Similar to the Google Shopping example above, to follow the SRP, we will need to put these steps into their separate class.

<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class DataImputation:
    def median_fill(self, data):
        """
        Code to fill missing data by median of feature
        """
        pass

class OutlierRemoval:
    def remove_by_euclidean_dist(self, data):
        """
        Code to remove outliers using Euclidean distance
        """
        pass

class FeatureAnalysis:
    def pearson_corr_cal(self, data):
        """
        Code to calculate Pearson correlation scores between 
        input feature(s) and output label(s)
        """
        pass
```
</p></details>
</br>

However, I don't find this principle helpful in a Kaggle or data science project, as each Jupyter Notebook cell can be run and tested individually.

## <span style="color:#286EE0">O</span>pen-Closed Principle

**OCP**: *"A module (or component) should be open for extension but closed for modification"* — Bertrand Meyer. When making changes, the principle prevents the already functional design from bugs or breaks. This principle promotes a modular and flexible design that allows for the easy integration of a new idea while making your codebase more maintainable and scalable. The OCP can be hard to understand, so let's walk through some examples.

<center>
    <img style="width: 50%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/solid_principles/imgs/cartoons/code_reminiscing_cartoon.png" />
</center>
<figcaption class="img_footer">
    Fig. 3. Sometime it is hard to implement new features without refactor the code.</br>
    (Image source: 
    <a href="https://www.monkeyuser.com/2018/reminiscing/" class="img_footer">MonkeyUser.com</a>).
</figcaption>


### Web Development Example
An easy-to-see symptom of OCP violation to look for is the use of `if/elif/else` or `switch-case` statements. Let's say that you are a (Flask or Django) backend developer at Meta who is writing a REST API that uses HTTP request protocols (POST, GET, PUT, DELETE) to allow users to interact with the database via CRUD (Create, Read, Update, Delete).

<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class RequestHandler:
    def handle_request(self, request):
        """
        Code to handle request based on type
        """
        if request.method == "GET":
            self.handle_get(request)
        elif request.method == "POST":
            self.handle_post(request)
        elif request.method == "PUT":
            self.handle_put(request)
        elif request.method == "DELETE":
            self.handle_delete(request)

    def handle_get(self, request):
        """
        Code to handle GET request
        """
        pass

    def handle_post(self, request):
        """
        Code to handle POST request
        """
        pass

    def handle_put(self, request):
        """
        Code to handle PUT request
        """
        pass

    def handle_delete(self, request):
        """
        Code to handle DELETE request
        """
        pass
```
</p></details>
</br>

The example above violates OCP because every time a new request type is added (e.g., PATCH), our `RequestHandler` class needs to be modified. This can introduce new bugs into existing code. As the OCP stated, we should design our code to be fixed but extended.

**Fix:** A solution to OCP violation is to separate each request type into individual classes, thus abstracting the `RequestHandler` class. Therefore, if we want to add a PATCH request, we can extend our API by adding a new `PatchRequestHander` class.

<center>
    <img style="width: 90%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/solid_principles/imgs/diagrams/ocp.png" />
</center>
<figcaption class="img_footer">
    Fig. 4. Design refactored with open-closed principle.
</figcaption>

</br>

<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class RequestHandler:
    def handle_request(self, request):
        """
        Code to handle request based on type
        """
        request.handle()

class GetRequestHandler:
    def handle(self):
        """
        Code to handle GET request
        """
        pass

class PostRequestHandler:
    def handle(self):
        """
        Code to handle POST request
        """
        pass

class PutRequestHandler:
    def handle(self):
        """
        Code to handle PUT request
        """
        pass

class DeleteRequestHandler:
    def handle(self):
        """
        Code to handle DELETE request
        """
        pass

class PatchRequestHandler:
    def handle(self):
        """
        Code to handle PATCH request (extended)
        """
        pass
```
</p></details>
</br>

### Data Science Example

Let's say you are a Machine Learning Engineer at NVIDIA who is writing a Python script for a baseline model with data preprocessing, model training, and model evaluation. Like the REST API example above, you want your class `ModelPipeline` to remain closed for modification but open for extension by strictly following the OCP.

<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class DataPreprocessor:
    def preprocess(self, dataset):
        """
        Code to preprocess data
        """
        pass

class ModelTrainer:
    def train(self, dataset):
        """
        Code to train model
        """
        pass

class ModelEvaluator:
    def evaluate(self, model, dataset):
        """
        Code to evaluate model
        """
        pass

class ModelPipeline:
    def __init__(self, preprocessor, trainer, evaluator):
        """
        Code to build a ModelPipeline constructor (object)
        """
        self.preprocessor = preprocessor
        self.trainer = trainer
        self.evaluator = evaluator

    def run_pipeline(self, dataset):
        """
        Code to run the machine learning project end-to-end
        """
        preprocessed_data = self.preprocessor.preprocess(dataset)
        model = self.trainer.train(preprocessed_data)
        evaluation_result = self.evaluator.evaluate(model, preprocessed_data)
        return evaluation_result
```
</p></details>
</br>

Your teammate develops a new way of processing the dataset. Luckily, due to your guideline of OCP, your teammate can easily extend the existing baseline model by inheriting the `DataPreprocessor` class without the risk of breaking your functional baseline design.

<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class NewDataPreprocessor(DataPreprocessor):
    def preprocess(self, dataset):
        """
        Code to preprocess data with new technique
        """
        pass
```
</p></details>
</br>

## <span style="color:#286EE0">L</span>iskov Substitution Principle

**LSP**: *"Subclasses should be substitutable for their base classes (without affecting the correctness of the program)"* — Barbara Liskov. In OOP, what we want is for any method or code that works for a base class should continue to work correctly when used with the derived types. This principle ensures the inheritance hierarchies are consistent, extensible, and correct.

<center>
    <img style="width: 50%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/solid_principles/imgs/cartoons/code_reuse_cartoon.png" />
</center>
<figcaption class="img_footer">
    Fig. 5. Design your codebase to be more predictable for later reuse.</br> 
    (Image source: 
    <a href="https://www.monkeyuser.com/2018/code-reuse/" class="img_footer">MonkeyUser.com</a>).
</figcaption>

### Web Development & Data Science Example
Let's say that you are to design a codebase at Netflix to write processed data into a MySQL database and a CSV file (You can think of adding new columns into a database by scraping or engineering new features).

<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class DataHandler():
    def write_db(self, data):
        """
        Code to write processed data to MySQL database
        """
        print("Handling MySQL database.")

    def write_csv(self, data):
        """
        Code to write processed data to CSV file
        """
        print("Handling CSV file.")

class WriteDB(DataHandler):
    def write_db(self, data):
        """
        Code to write processed data to MySQL database
        """
        print("Handling MySQL database.")

    def write_csv(self, data):
        """
        Code to write processed data to CSV file
        """
        raise Exception("Error: Can't write to CSV file.") 

class WriteCSV(DataHandler):
    def write_db(self, data):
        """
        Code to write processed data to MySQL database
        """
        raise Exception("Error: Can't write to MySQL database.") 

    def write_csv(self, data):
        """
        Code to write processed data to CSV file
        """
        print("Handling CSV file.")
```
</p></details>
</br>

Here, our base class `DataHandler` defined two methods, `write_db()` and `write_csv()`. The derived class `WriteDB` inherits from `DataHander` and overrides the write_csv method. However, instead of providing the expected behavior, it prints an error message indicating it can't write to a CSV file. Similarly, the derived class `WriteCSV` prints out the error message indicating it can't write to MySQL file. This design violates the LSP as the derived classes do not behave as expected based on the contract defined by the `DataHandler` base class. The base class is designed to be too specific, thus causing its children to handle edge case(s) based on the characteristics of the child classes.


**Fixed:** Let's write a more generic base class!

<center>
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/solid_principles/imgs/diagrams/lsp.png" />
</center>
<figcaption class="img_footer">
    Fig. 6. Design refactored with liskov substitution principle.
</figcaption>

</br>

<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class DataHandler():
    def write(self, data):
        """
        Code to handle processed data
        """
        print("Handling data.")

class WriteDB(DataHandler):
    def write(self, data):
        """
        Code to write processed data to MySQL database
        """
        print("Handling MySQL database.")

class WriteCSV(DataHandler):
    def write(self, data):
        """
        Code to write processed data to CSV file
        """
        print("Handling CSV file.")
```
</p></details>
</br>

If you have an object of type `WriteDB` or `WriteCSV`, you can safely use it wherever an object of type `DataHandler` is expected because they adhere to the same contract. 

## <span style="color:#286EE0">I</span>nterface Segregation Principle


**ISP**: *"Many client-specific interfaces are better than one general purpose interface"* — Robert C. Martin.  If we have an extensive interface with many functions, the class implementing the interface might only use some defined functions! It is better to break up the interface into multiple smaller interfaces; then, we can inherit our class's needed interface(s). This principle promotes code modularity, reduces unnecessary dependencies, and makes it easier to maintain/extend the existing codebase.

<center>
    <img style="width: 50%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/solid_principles/imgs/cartoons/code_features_cartoon.png" />
</center>
<figcaption class="img_footer">
    Fig. 7
    . Extensive class can be hard to be refactored, inherited, or reused.</br>
    (Image source: 
    <a href="https://www.monkeyuser.com/2020/features/" class="img_footer">MonkeyUser.com</a>).
</figcaption>

### Web Development Example
Let's say you are a Full-stack Web Developer at Odoo who writes a simple web app with a home page and admin page.

<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class WebPage:
    def render(self):
        """
        Code to render HTML of a generic web page
        """
        pass

    def save(self):
        """
        Code to save data of a generic web page into a database
        """
        pass

    def delete(self):
        """
        Code to delete data of a generic web page from a database
        """
        pass

class HomePage(WebPage):
    def render(self):
        """
        Code to render HTML of home page
        """
        pass

    def save(self):
        """
        Code to save data of home page into a database
        """
        pass

    def delete(self):
        """
        Code to delete data of home page from a database
        """
        raise Exception("Error: Only Admin can delete data from database.") 

class AdminPage(WebPage)
    def render(self):
        """
        Code to render HTML of admin page
        """
        pass

    def save(self):
        """
        Code to save data of admin page into a database
        """
        pass

    def delete(self):
        """
        Code to delete data of admin page from a database
        """
        pass
```
</p></details>
</br>

The example above violates the ISP because the children should not be forced to depend on the parent's method(s) they do not use. While the `AdminPage` class inherits just fine, the `HomePage` class can't use the `delete()` function. This creates an unnecessary dependency!


**Fixed:** It will be better to segregate the parent (`WebPage`) class into smaller interface(s) that meet the needs of each child. We can separate `render()`, `save()`, and `delete()` functions into multiple classes.

<center>
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/solid_principles/imgs/diagrams/isp.png" />
</center>
<figcaption class="img_footer">
    Fig. 8. Design refactored with interface segregation principle.
</figcaption>

</br>

<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class Renderable:
    def render(self):
        """
        Code to render HTML of a generic web page
        """
        pass

class Savable:
    def save(self):
        """
        Code to save data of a generic web page into a database
        """
        pass

class Deletable:
    def delete(self):
        """
        Code to delete data of a generic web page from a database
        """
        pass

class HomePage(Renderable, Savable):
    def render(self):
        """
        Code to render HTML of home page
        """
        pass

    def save(self):
        """
        Code to save data of home page into a database
        """
        pass

class AdminPage(Renderable, Savable, Deletable):
    def render(self):
        """
        Code to render HTML of admin page
        """
        pass

    def save(self):
        """
        Code to save data of admin page into a database
        """
        pass

    def delete(self):
        """
        Code to delete data of admin page from a database
        """
        pass
```
</p></details>
</br>

### Data Science Example

Let's say that you are a Data Scientist at LinkedIn who is working on a multimodal application. You are tasked to process image and text data. Like the web development example above, you want separate interfaces for each subtask and inherit related interfaces to process images and text accordingly.

<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class DataLoader:
    def load(self, data):
        """
        Code to load data to notebook memory (entire dataset or as a generator)
        """
        pass

class DuplicateRemoval:
    def remove_dup(self, data):
        """
        Code to remove duplicate images in the dataset
        """
        pass

class DataAugmentation:
    def img_augment(self, data):
        """
        Code to augment images in the dataset
        """
        pass

class DataSmoothing:
    def ts_smooth(self, data):
        """
        Code to smooth time-series dataset
        """
        pass

class ProcessTimeSeriesDataset(DataLoader, DataSmoothing):
    def load(self, data):
        """
        Code to load data to notebook memory (entire dataset or as a generator)
        """
        pass

    def ts_smooth(self, data):
        """
        Code to smooth time-series dataset
        """
        pass

class ProcessImageDataset(DataLoader, DuplicateRemoval, DataAugmentation):
    def load(self, data):
        """
        Code to load data to notebook memory (entire dataset or as a generator)
        """
        pass

    def remove_dup(self, data):
        """
        Code to remove duplicate images in the dataset
        """
        pass

    def img_augment(self, data):
        """
        Code to augment images in the dataset
        """
        pass
```
</p></details>
</br>

Here, we have the defined separate interfaces for data load, removing duplicates, image augmentation, and time-series smoothing. The `ProcessTimeSeriesDataset` and `ProcessImageDataset` classes only implement (or inherit) the interfaces (or parent classes) that are relevant to them.

## <span style="color:#286EE0">D</span>ependency Inversion Principle

**DIP**: *"Depend on abstractions. Do not depend on concretions"* — Robert C. Martin. The main idea is to decouple high-level modules from low-level modules by introducing abstractions as mediators. When integrating external dependencies, it is better to create wrapper(s) around them so that your code depends on the wrapper you make and not the details of the dependencies. This allows for better flexibility, as different implementations can be easily substituted without affecting the high-level modules. This principle promotes modularity and maintainability in codebase design.

<center>
    <img style="width: 50%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/solid_principles/imgs/cartoons/code_implementation_cartoon.png" />
</center>
<figcaption class="img_footer">
    Fig. 9. Create a wrapper and hide the details. Not everyone need to know all the nitty-gritty of the system (Image source: 
    <a href="https://www.monkeyuser.com/2018/implementation/" class="img_footer">MonkeyUser.com</a>).
</figcaption>

### Web Development Example
Let's say you are a Mobile Developer at Apple who work on the payment integration aspect of Apple Music. Your task is to integrate Stripe Payment API into your backend codebase.
<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class StripeProcessor:
    def process_payment(self, credit_cart_num):
        """
        Code to process payment via Stripe Payment API
        """
        pass

class AppleMusic:   
    def notify_payment(self, credit_cart_num):
        """
        Code to process payment in iOS backend
        """
        processor = StripeProcessor()
        processor.process_payment(credit_cart_num)
```
</p></details>
</br>

The Apple Music example above violates DIP as the `AppleMusic` class directly depends on `StripeProcessor` class, a specific low-level implementation. Imagine that Stripe provides Stripe Payment API version 2.0, which has a massive change in multiple methods. Our `AppleMusic` (and any other class that uses the `StripeProcessor` object) will be broken. We will have to fix every single line that uses `StripeProcessor`'s methods.

**Fixed:** `AppleMusic` and `StripeProcessor` classes should depend on abstractions (or a wrapper for StripeProcessor) to avoid such catastrophe. In addition, we can easily swap the external API (e.g., Venmo Payment API) within the wrapper class by having a wrapper.

<center>
    <img style="width: 70%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/solid_principles/imgs/diagrams/dip.png" />
</center>
<figcaption class="img_footer">
    Fig. 10. Design refactored with dependency inversion principle.
</figcaption>

</br>

<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class PaymentProcessor:
    def process_payment(self, credit_cart_num):
        """
        Code to process payment via external API
        """
        pass

class StripeProcessor(PaymentProcessor):
    def process_payment(self, credit_cart_num):
        """
        Code to process payment via Stripe Payment API
        """
        pass

class VenmoProcessor(PaymentProcessor):
    def process_payment(self, credit_cart_num):
        """
        Code to process payment via Venmo Payment API
        """
        pass

class AppleMusic:
    def __init__(self, processor: PaymentProcessor):
        """
        Code to build AppleMusic constructor (object)
        """
        self.processor = processor

    def notify_payment(self, credit_cart_num):
        """
        Code to process payment in iOS backend
        """
        self.processor.process_payment(credit_cart_num)
```
</p></details>
</br>

### Data Science Example
Let's say you are a Data Analyst at Deloitte who is in charge of plotting the dataset to show insight to stakeholders. Similarly to the Apple Music example above, creating a wrapper for the data visualization task would be best.

<details open><summary>
<span style="color:#286EE0">Code Example</span>
</summary><p>

```python
class Plotter:
    def show_plots(self, dataset):
        """
        Code to plot the dataset
        """
        pass

class SeabornPlotter(Plotter):
    def show_plots(self, dataset):
        """
        Code to plot the dataset bia Seaborn API
        """
        pass


class PlotlyPlotter(Plotter):
    def show_plots(self, dataset):
        """
        Code to plot the dataset bia Plotly API
        """
        pass

class BusinessInsight():
    def __init__(self, plotter: Plotter):
        """
        Code to build BusinessInsight constructor (object)
        """
        self.plotter = plotter

    def notify_payment(self, dataset):
        """
        Code to show the visualization trends or patterns of the dataset
        """
        self.plotter.show_plots(dataset)
```
</p></details>
</br>

Here, the `BusinessInsight` class depends on the `Plotter` abstraction through its constructor, allowing different plotting implementations to be injected without modifying the `BusinessInsight` class. The `Plotter` class serves as the abstraction, while `SeabornPlotter` and `PlotlyPlotter` are concrete implementations of the `Plotter` class. Depending on the abstraction (`Plotter`), the `BusinessInsight` class is decoupled from specific plotting implementations. This promotes flexibility and modularity, as different plotting libraries or variations can be used interchangeably by appropriately implementing the `Plotter` abstraction to the `BusinessInsight` class.


## Citation
Cited as:

<blockquote>
    <summary>Nguyen, Minh. (May 2023). S.O.L.I.D Principles Explained.</summary>
    <summary>https://mnguyen0226.github.io/posts/solid_principles/post/.</summary>
</blockquote>

Or 

```sh
@article{nguyen2023solid,
  title   = "S.O.L.I.D Principles Explained.",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "April",
  url     = "https://mnguyen0226.github.io/posts/solid_principles/post/"
}
```

## References

[1] R. S. Pressman and B. R. Maxim, Software Engineering: A Practitioner’s Approach. New York, NY: McGraw-Hill Education, 2020. 

[2] R. C. Martin, M. C. Feathers, T. R. Ottinger, and J. J. Langr, Clean Code A Handbook of Agile Software Craftsmanship. Boston, MA: Pearson Education, Inc, 2016. 

[3] R. C. Martin, “Clean Code - Lecture Series,” YouTube, https://www.youtube.com/watch?v=7EmboKQH8lM&amp;list=PLwAjnlpkQEft41G-GvHAKnh_CkaEKFawh&amp;ab_channel=UnityCoin (accessed May 12, 2023). 

[4] “SOLID Design Principle - Web Dev Simplified,” YouTube, https://www.youtube.com/watch?v=UQqY3_6Epbg&amp;list=PLZlA0Gpn_vH9kocFX7R7BAe_CvvOCO_p9&amp;ab_channel=WebDevSimplified (accessed May 12, 2023).

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/solid_principles/imgs/hcm_city_unsplash.jpg" />
</center>
<figcaption class="img_footer">
    Fig. 11. Ho Chi Minh City, Viet Nam. (Image source: 
    <a href="https://unsplash.com/photos/75rWOqdKCdM" class="img_footer">Peter Nguyen @ Unsplash</a>).
</figcaption>

<!-- CSS Styling -->
<style>
.img_size {
  width: 100%;
}

.img_footer {
    color: #888888;
    text-align: center;
}
</style>