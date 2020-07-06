<p align="center">
  <a href="https://hultner.se/"><img src="https://hultner.se/img/logo/logo_black-01.svg" alt="Hultnér Technologies" align="center" width="200"></a>
</p>
<p align="center">
	<a href="https://hultner.se/" rel="nofollow" class="rich-diff-level-one">Hultnér Technologies AB</a> | <a href="https://twitter.com/ahultner" rel="nofollow" class="rich-diff-level-one">@ahultner</a> | <a href="http://alexander.hultner.se" rel="nofollow" class="rich-diff-level-one">Blog</a> | <a href="https://slides.com/hultner/" rel="nofollow" class="rich-diff-level-one">Slides</a> | <a href="https://www.facebook.com/groups/nordiskpython/" rel="nofollow" class="rich-diff-level-one">Nordisk Python Community</a> | <a href="https://github.com/hultner-technologies/Schema-based-API-Testing/" rel="nofollow" class="rich-diff-level-one">GitHub</a>
	<hr>
</p>

# ⠠⠵ Schema-based-API-Testing
**Automatically generate test-cases based on your API-schemas.**  

The goal with this talk is to introduce the audience to property-based testing for API’s using schemas to automatically generate test scenarios, enabling them to write more powerful tests faster.

The talk will focus on a subset of the field of property-based testing where we focus on testing by automatically generating properties and test strategies from the API Schemas that we often already have. These tests ensure that our APIs conform to their specified schema and enables us to write a much larger amount of tests in less time.

I will focus on the schemathesis library which leverages the strong hypothesis library as well as the hypothesis-JSONSchema extension strategies, and will in the future also support GraphQL via the hypothesis-graphql strategies. I’m a contributor to schemathesis and currently working on the future GraphQL support with schemathesis creator, Dmitry Dygalo.

I will also compare it with its predecessor “swagger-conformance”, pure property-based testing through hypothesis, schema strategies with hypothesis-graphql and hypothesis-jsonschema, and discuss their advantages and disadvantages. I will also briefly talk about “QuickREST: Property-based Test Generation of OpenAPI-Described RESTful APIs” (https://arxiv.org/abs/1912.09686), the research paper that’s part of the inspiration for these tools.

By focusing on property-based test generation using schemas we already have, I will show that a field like property-based testing, which can seem quite daunting at first, actually can have a low barrier to entry while yielding large amounts of value in return and is useful for most common web projects today.

The talk will show how formal schemas for APIs can and will continue to provide additional value outside the scope of documentation.


## ⠠⠵ Quick reference

### CLI
```shell
$ schemathesis run http://127.0.0.1:5000/swagger.json
    
================== Schemathesis test session starts ==================
platform …
rootdir: /~/dev/hultner_technologies/Schema-based-API-Testing/code
hypothesis profile 'default' -> database=Directory…
Schema location: http://127.0.0.1:5000/swagger.json
Base URL: http://127.0.0.1:5000/
Specification version: Swagger 2.0
Workers: 1
collected endpoints: 5

GET /todos/ .                                                  [ 20%]
POST /todos/ .                                                 [ 40%]
DELETE /todos/{id} .                                           [ 60%]
GET /todos/{id} .                                              [ 80%]
PUT /todos/{id} .                                              [100%]

============================== SUMMARY ===============================

Performed checks:
    not_a_server_error                    500 / 500 passed          PASSED

========================= 5 passed in 5.32s ==========================
```
### Via pytest
```python
# Minimal usage example
import requests
import schemathesis

schema = schemathesis.from_uri("http://0.0.0.0:8080/swagger.json")

@schema.parametrize()
def test_no_server_errors(case):
    # `requests` will make an appropriate call under the hood
    response = case.call()  # use `call_wsgi` if you used `schemathesis.from_wsgi`
    # You could use built-in checks
    case.validate_response(response)
    # Or assert the response manually
    assert response.status_code < 500
```

## Talks
### ⠠⠵ FlaskCon, 2020 July 5
- Type: Talk (20 mins)
- [Schedule](https://flaskcon.com/#schedule_section)
- Video: TBA
- [Slides](https://slides.com/hultner/flaskcon2020)

### ⠠⠵ EuroPython, 2020 July 23
- Type: Talk (30 mins)
- Python level: Intermediate
- Domain level: Intermediate
- [Schedule](https://ep2020.europython.eu/schedule/23-july?selected=8XYc942-api-schema-based-testing-with-schemathesis)
- [Details on europython.eu](https://ep2020.europython.eu/talks/8XYc942-api-schema-based-testing-with-schemathesis/)



## ⠠⠵ FAQ, pydantic
**Stateful testing?**  
[Yes](https://schemathesis.readthedocs.io/en/stable/stateful.html), using links.

**GraphQL?**  
[In-progress](https://schemathesis.readthedocs.io/en/stable/graphql.html), check link for latest progress.

**OpenAPI, Swagger?**  
Yes, Schemathesis supports both the older Swagger 2.0 standard and the newer OpenAPI 3 standard

**Incompabilities?**
Can be addressed using [fixups](https://schemathesis.readthedocs.io/en/stable/compatibility.html?highlight=fixup), a built in fixup for FastAPI is included.  
Activate in CLI with: `--fixups=all`

**I have a question not covered here, where can I ask it?**  
I'm [@ahultner on twitter](https://twitter.com/ahultner), otherwise you can also email me (address in slides).

## ⠠⠵ Links
- Schemathesis
- Hypothesis, Talk, Course, Docs
- [Flask](https://flask.palletsprojects.com/en/1.1.x/), [RestX](https://github.com/python-restx/flask-restx)[RESTPlus](https://flask-restplus.readthedocs.io/en/stable/)
- [FastAPI](https://fastapi.tiangolo.com)
- [QuickREST Paper](https://arxiv.org/abs/1912.09686)

