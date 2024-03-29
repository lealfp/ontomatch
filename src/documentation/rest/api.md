# Ontomatch REST-based service

This service parses a given text and returns entities (URIs) of an ontology.

Available **ontology IDs**
[`pato`](https://bioportal.bioontology.org/ontologies/HFO),
[`tao`](https://bioportal.bioontology.org/ontologies/HFO),
[`xao`](https://bioportal.bioontology.org/ontologies/HFO),
[`hfo`](https://bioportal.bioontology.org/ontologies/HFO)


### Based on a given similarity threshold (/api/rest/resource)


* **URL:**    `/api/rest/resource`

* **Method:**  `POST`
  
*  **Required POST Params:**

   * `text=[string]`
   * `similarity=[float]` [between 0 and 1]
   * `ontology=[ontologyID]` [see ontology IDs]
     

* **Success Response:**

  * **Code:** 200 <br />
  * **Content:** JSON object <br />

* **Error Responses:**

  * **Code:** `415 Unsupported Media Type` <br />
    **Troubleshooting:** Check parameters


  * **Code:**  `404 NOT FOUND`  <br />
    **Troubleshooting:**  Ontology ID not found

* **Sample Call:**
  
    * **Code:** 
  ```javascript
    $.ajax({
      url: "http://ontomatch.lis.ic.unicamp.br/api/rest/resource",
      dataType: "json",
      type : "POST",
      data: { text: "chest pain", similariy: 0.8, ontology:"hfo" },
      success : function(r) {
        console.log(r);
      }
    });
  ```

    * **Return:**  `{"uri":"http://bmi.utah.edu/ontologies/hfontology/C0008031","label":"Chest Pain","similarity":1.0}`






### Based on a given similarity threshold (/api/rest/resources)


* **URL:**    `/api/rest/resource`

* **Method:**  `POST`
  
*  **Required POST Params:**

   * `text=[string]`
   * `n=[float]` [the service will return the **n** most similar entities]
   * `ontology=[ontologyID]` [see ontology IDs]
     

* **Success Response:**

  * **Code:** 200 <br />
  * **Content:** JSON array <br />

 
* **Error Responses:**

  * **Code:** `415 Unsupported Media Type` <br />
    **Troubleshooting:** Check parameters


  * **Code:**  `404 NOT FOUND`  <br />
    **Troubleshooting:**  Ontology ID not found

* **Sample Call:**
  
    * **Code:** 
  ```javascript
    $.ajax({
      url: "http://ontomatch.lis.ic.unicamp.br/api/rest/resources",
      dataType: "json",
      type : "POST",
      data: { text: "chest pain", n: 5, ontology:"hfo" },
      success : function(r) {
        console.log(r);
      }
    });
  ```

    * **Return:**  

    ```json
    [
    {"uri":"http://bmi.utah.edu/ontologies/hfontology/C0008031","label":"Chest Pain","similarity":1.0},
    {"uri":"http://bmi.utah.edu/ontologies/hfontology/C0030193","label":"Pain","similarity":0.7071067690849304},
    {"uri":"http://bmi.utah.edu/ontologies/hfontology/C0000737","label":"Abdominal Pain","similarity":0.5}
    ]
    ```
