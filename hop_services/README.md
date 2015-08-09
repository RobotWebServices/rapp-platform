## Synopsis

Containes RAPP Platform web services developed using hOP web broker.
These services are used in order to communicate with the RAPP Platform echosystem
and access RIC(RAPP Improvement Center) AI modules.

## Directories

- services/ : Front-end HOP services running on RAPP Platform.
- utilities/ : General Utilities used for developing and testing HOP services. 

## Services

- **qr_detection ( {file_uri: ''} )**

  **Input parameters**

  - file_uri: Destination where the posted file data (**image file**) are saved by hop-server.
    Data are posted using a multipart/form-data post request using this field.
    e.g.
    ```python
    file = {'file_uri': open(<to-send-file-path>, 'rb')}
    ```

  **Response/Return-Data**
  The returned data are in *JSON* representation. A JSON.load() from client side must follow in order to decode
  the received datia.

  > { qr_centers: [], error: '' }

  - qr_centers: Dynamic vector that containes points (x,y,z) of found QR in an image frame.
  - error: If error was encountered, an error message is pushed in this field
    and returned to the client.

  > {
  >   qr_centers: [ { y: 165, x: 165, z: 0 } ],
  >   error: '<error_mesasge>'
  > }




- **face_detection ( {file_uri: ''} )**

  **Input parameters**

  - file_uri: Destination where the posted file data (**image file**) are saved by hop-server.
    Data are posted using a multipart/form-data post request using this field.
    e.g.
    ```python
    file = {'file_uri': open(<to-send-file-path>, 'rb')}
    ```

  **Response/Return-Data**

  The returned data are in *JSON* representation. A JSON.load() from client side must follow in order to decode
  the received datia.

  > { faces_up_left: [], faces_down_right: [], error: '' }

  - faces_up_left: Dynamic vector that containes points (x,y,z) of recognized faces in an image frame.
  - faces_down_right: Dynamic vector that containes points (x,y,z) of recognized faces in an image frame.
  - error: If error was encountered, an error message is pushed in this field
    and returned to the client.

  > {
  >   faces_up_left: [ { y: 200, x: 212, z: 0 } ],
  >   faces_down_right: [ { y: 379, x: 391, z: 0 } ],
  >   error: '<error_message>'
  > }


- **set_denoise_profile ( {file_uri: '', audio_source: '', user: ''} )**

  **Input parameters**

  - **'file_uri'**: Destination where the posted file data (**audio data file**) are saved by hop-server.
    Data are posted using a multipart/form-data post request using this field.
    e.g.
    ```python
    file = {'file_uri': open(<to-send-file-path>, 'rb')}
    ```

  - **'audio_source'**: A value that presents the <robot>_<encode>_<channels> information for the audio source data.
    e.g "nao_wav_1_ch".
  - **'user'**: User’s name. Used for per-user profile denoise configurations.
    e.g "klpanagi"


  **Response/Return-Data**

  The returned data are in *JSON* representation. A JSON.load() from client side must follow in order to decode
  the received datia.

  > { error: '<error_message>' }

  - error: If error was encountered, an error message is pushed in this field
    and returned to the client.

  > {
  >  error:"RAPP Platform Failure!"
  > }


- **speech_detection_sphinx4 ( { file_uri: '', language: '',
    audio_source: '', words: [], sentences: [], grammar: [], user: ''
    })**

  **Input parameters**

  - **'file_uri'**: Destination where the posted file data (**audio data file**) are saved by hop-server.
    Data are posted using a multipart/form-data post request using this field.
    e.g.
    ```python
    file = {'file_uri': open(<to-send-file-path>, 'rb')}
    ```

  - **'language'**: Language to be used by the speech_detection_sphinx4 module.
    Currently valid language values are ‘gr’ for Greek and ‘en’ for English.
  - **'audio_source'**: A value that presents the <robot>_<encode>_<channels> information for the audio source data.
    e.g "nao_wav_1_ch".
  - **'words[]'**: A vector that carries the words to search for into the voice-audio-source.
  - **'sentences[]'**: The under consideration sentences.
  - **'grammar[]'**: Grammars to use in speech recognition.
  - **'user'**: User’s name. Used for per-user profile denoise configurations.
    e.g "klpanagi"


  **Response/Return-Data**

  The returned data are in *JSON* representation. A JSON.load() from client side must follow in order to decode
  the received datia.

  > { words: [], error: '<error_message>' }

  - **'error'**: If error was encountered, an error message is pushed in this field
    and returned to the client.
  - **'words[]'**: A vector that contains the "words-found"



- **ontology_subclasses_of ( { query: ''} )**

  **Input parameters**

  - **'query'**: The query to the ontology database.


  **Response/Return-Data**

  The returned data are in *JSON* representation. A JSON.load() from client side must follow in order to decode
  the received datia.

  > { results: [], trace: [], error: '<error_message>' }

  - **'results'**: Query results returned from ontology database.
  - **'trace'**:
  - **'error'**: If error was encountered, an error message is pushed in this field
    and returned to the client.

  > { [ 'http://knowrob.org/kb/knowrob.owl#Oven',
  >     'http://knowrob.org/kb/knowrob.owl#MicrowaveOven',
  >     'http://knowrob.org/kb/knowrob.owl#RegularOven',
  >     'http://knowrob.org/kb/knowrob.owl#ToasterOven'],
  >   [],
  >   ''
  > }


- **ontology_superclasses_of ( { query: ''} )**

  **Input parameters**

  - **'query'**: The query to the ontology database.


  **Response/Return-Data**

  The returned data are in *JSON* representation. A JSON.load() from client side must follow in order to decode
  the received datia.

  > { results: [], trace: [], error: '<error_message>' }

  - **'results'**: Query results returned from ontology database.
  - **'trace'**:
  - **'error'**: If error was encountered, an error message is pushed in this field
    and returned to the client.


- **ontology_is_subsuperclass_of ( { parent_class: '', child_class: '', recursive: false } )**

  **Input parameters**

  - **'parent_class'**: The parent class name.
  - **'child_class'**: The child class name.
  - **'recursive'**: Defines if a recursive procedure will be used (true/false).


  **Response/Return-Data**

  The returned data are in *JSON* representation. A JSON.load() from client side must follow in order to decode
  the received datia.

  > { results: [], trace: [], error: '<error_message>' }

  - **'results'**: Query results returned from ontology database.
  - **'trace'**:
  - **'error'**: If error was encountered, an error message is pushed in this field
    and returned to the client.



## Tests

Developed tests and testing tools are currently located under:
```
utilities/testing_tools/
```

## Contributors

- Konstaninos Panayiotou, **[klpanagi@gmail.com]**
- Manos Tsardoulias, **[etsardou@gmail.com]**
- Vincent Prunet, **[vincent.prunet@inria.fr]**