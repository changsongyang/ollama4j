---
sidebar_position: 1
---

# Models from Ollama Library

These API retrieves a list of models directly from the Ollama library.

### List Models from Ollama Library

This API fetches available models from the Ollama library page, including details such as the model's name, pull count,
popular tags, tag count, and the last update time.

<iframe style={{ width: '100%', height: '919px', border: 'none' }} allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Follama4j%2Follama4j-examples%2Fblob%2Fmain%2Fsrc%2Fmain%2Fjava%2Fio%2Fgithub%2Follama4j%2Fexamples%2FListLibraryModels.java&style=default&type=code&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on" />

<a href="https://github.com/ollama4j/ollama4j-examples/blob/main/src/main/java/io/github/ollama4j/examples/ListLibraryModels.java" target="_blank">
  View ListLibraryModels.java on GitHub
</a>

The following is the sample output:

```
[
    LibraryModel(name=llama3.2-vision, description=Llama 3.2 Vision is a collection of instruction-tuned image reasoning generative models in 11B and 90B sizes., pullCount=21.1K, totalTags=9, popularTags=[vision, 11b, 90b], lastUpdated=yesterday), 
    LibraryModel(name=llama3.2, description=Meta's Llama 3.2 goes small with 1B and 3B models., pullCount=2.4M, totalTags=63, popularTags=[tools, 1b, 3b], lastUpdated=6 weeks ago)
]
```

### Get Tags of a Library Model

This API Fetches the tags associated with a specific model from Ollama library.

```java title="GetLibraryModelTags.java"
import io.github.ollama4j.OllamaAPI;
import io.github.ollama4j.models.response.LibraryModel;
import io.github.ollama4j.models.response.LibraryModelDetail;

public class Main {

    public static void main(String[] args) {

        String host = "http://localhost:11434/";

        OllamaAPI ollamaAPI = new OllamaAPI(host);

        List<LibraryModel> libraryModels = ollamaAPI.listModelsFromLibrary();

        LibraryModelDetail libraryModelDetail = ollamaAPI.getLibraryModelDetails(libraryModels.get(0));

        System.out.println(libraryModelDetail);
    }
}
```

The following is the sample output:

```
LibraryModelDetail(
  model=LibraryModel(name=llama3.2-vision, description=Llama 3.2 Vision is a collection of instruction-tuned image reasoning generative models in 11B and 90B sizes., pullCount=21.1K, totalTags=9, popularTags=[vision, 11b, 90b], lastUpdated=yesterday), 
  tags=[
        LibraryModelTag(name=llama3.2-vision, tag=latest, size=7.9GB, lastUpdated=yesterday), 
        LibraryModelTag(name=llama3.2-vision, tag=11b, size=7.9GB, lastUpdated=yesterday), 
        LibraryModelTag(name=llama3.2-vision, tag=90b, size=55GB, lastUpdated=yesterday)
    ]
)
```

### Find a model from Ollama library

This API finds a specific model using model `name` and `tag` from Ollama library.

```java title="FindLibraryModel.java"
import io.github.ollama4j.OllamaAPI;
import io.github.ollama4j.models.response.LibraryModelTag;

public class Main {

    public static void main(String[] args) {

        String host = "http://localhost:11434/";

        OllamaAPI ollamaAPI = new OllamaAPI(host);

        LibraryModelTag libraryModelTag = ollamaAPI.findModelTagFromLibrary("qwen2.5", "7b");

        System.out.println(libraryModelTag);
    }
}
```

The following is the sample output:

```
LibraryModelTag(name=qwen2.5, tag=7b, size=4.7GB, lastUpdated=7 weeks ago)
```

### Pull model using `LibraryModelTag`

You can use `LibraryModelTag` to pull models into Ollama server.

```java title="PullLibraryModelTags.java"
import io.github.ollama4j.OllamaAPI;
import io.github.ollama4j.models.response.LibraryModelTag;

public class Main {

    public static void main(String[] args) {

        String host = "http://localhost:11434/";

        OllamaAPI ollamaAPI = new OllamaAPI(host);

        LibraryModelTag libraryModelTag = ollamaAPI.findModelTagFromLibrary("qwen2.5", "7b");

        ollamaAPI.pullModel(libraryModelTag);
    }
}
```