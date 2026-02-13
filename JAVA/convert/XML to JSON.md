```java
/*
===========================================
ObjectMapper → ALL DTO MAPPING CASES
(JSON + XML + Map + Tree + String + Stream)
===========================================
*/

import com.fasterxml.jackson.core.type.TypeReference;
import com.fasterxml.jackson.databind.*;
import com.fasterxml.jackson.dataformat.xml.XmlMapper;

import java.io.InputStream;
import java.util.List;
import java.util.Map;

// ---------------- DTO ----------------
class UserDTO {
    public Long id;
    public String name;
}

// ---------------- MAIN EXAMPLES ----------------
public class ObjectMapperAllCases {

    public static void main(String[] args) throws Exception {

        // JSON ObjectMapper
        ObjectMapper jsonMapper = new ObjectMapper();

        // XML ObjectMapper
        XmlMapper xmlMapper = new XmlMapper();

        // ---------------------------------------
        // 1️⃣ JSON String → DTO
        // ---------------------------------------
        String json = "{\"id\":1,\"name\":\"Mohammed\"}";
        UserDTO user1 = jsonMapper.readValue(json, UserDTO.class);

        // ---------------------------------------
        // 2️⃣ JSON String → List<DTO>
        // ---------------------------------------
        String jsonList = "[{\"id\":1,\"name\":\"A\"},{\"id\":2,\"name\":\"B\"}]";
        List<UserDTO> users1 = jsonMapper.readValue(
                jsonList,
                new TypeReference<List<UserDTO>>() {}
        );

        // ---------------------------------------
        // 3️⃣ JSON String → Map
        // ---------------------------------------
        Map<String, Object> map1 = jsonMapper.readValue(
                json,
                new TypeReference<Map<String, Object>>() {}
        );

        // ---------------------------------------
        // 4️⃣ JSON → JsonNode (Tree Model)
        // ---------------------------------------
        JsonNode node = jsonMapper.readTree(json);
        String nameFromNode = node.get("name").asText();

        // ---------------------------------------
        // 5️⃣ JsonNode → DTO
        // ---------------------------------------
        UserDTO user2 = jsonMapper.treeToValue(node, UserDTO.class);

        // ---------------------------------------
        // 6️⃣ DTO → JSON String
        // ---------------------------------------
        String jsonOut = jsonMapper.writeValueAsString(user2);

        // ---------------------------------------
        // 7️⃣ Map → DTO
        // ---------------------------------------
        UserDTO user3 = jsonMapper.convertValue(map1, UserDTO.class);

        // ---------------------------------------
        // 8️⃣ DTO → Map
        // ---------------------------------------
        Map<String, Object> map2 = jsonMapper.convertValue(
                user3,
                new TypeReference<Map<String, Object>>() {}
        );

        // ---------------------------------------
        // 9️⃣ InputStream → DTO
        // ---------------------------------------
        InputStream is = ObjectMapperAllCases.class
                .getResourceAsStream("/user.json");

        UserDTO user4 = jsonMapper.readValue(is, UserDTO.class);

        // ---------------------------------------
        // 🔟 XML String → DTO
        // ---------------------------------------
        String xml = "<UserDTO><id>5</id><name>XML User</name></UserDTO>";
        UserDTO user5 = xmlMapper.readValue(xml, UserDTO.class);

        // ---------------------------------------
        // 1️⃣1️⃣ XML → List<DTO>
        // ---------------------------------------
        String xmlList =
                "<List>" +
                    "<UserDTO><id>1</id><name>A</name></UserDTO>" +
                    "<UserDTO><id>2</id><name>B</name></UserDTO>" +
                "</List>";

        List<UserDTO> users2 = xmlMapper.readValue(
                xmlList,
                new TypeReference<List<UserDTO>>() {}
        );

        // ---------------------------------------
        // 1️⃣2️⃣ XML → JsonNode
        // ---------------------------------------
        JsonNode xmlNode = xmlMapper.readTree(xml);
        String xmlName = xmlNode.get("name").asText();

        // ---------------------------------------
        // 1️⃣3️⃣ XML → DTO → JSON
        // ---------------------------------------
        UserDTO xmlUser = xmlMapper.readValue(xml, UserDTO.class);
        String xmlToJson = jsonMapper.writeValueAsString(xmlUser);

        // ---------------------------------------
        // 1️⃣4️⃣ Unknown fields (ignore safely)
        // ---------------------------------------
        jsonMapper.configure(
                DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES,
                false
        );

        // ---------------------------------------
        // 1️⃣5️⃣ Partial mapping (field extraction)
        // ---------------------------------------
        Long idOnly = node.get("id").asLong();

        // ---------------------------------------
        // 1️⃣6️⃣ Nested object mapping
        // ---------------------------------------
        String nestedJson =
                "{ \"user\": { \"id\": 9, \"name\": \"Nested\" } }";

        JsonNode nestedNode = jsonMapper.readTree(nestedJson);
        UserDTO nestedUser =
                jsonMapper.treeToValue(nestedNode.get("user"), UserDTO.class);

        // ---------------------------------------
        // 1️⃣7️⃣ Update existing DTO (merge)
        // ---------------------------------------
        UserDTO existing = new UserDTO();
        existing.id = 100L;

        jsonMapper.readerForUpdating(existing)
                .readValue("{\"name\":\"Updated\"}");

        // existing → { id:100, name:"Updated" }
    }
}

```

---
---

## 🧠 Mental Model (remember this)

|Input|Method|
|---|---|
|JSON/XML String|`readValue()`|
|JSON/XML → DTO|`readValue(..., DTO.class)`|
|JSON/XML → List|`TypeReference<List<T>>`|
|Any → DTO|`convertValue()`|
|Any → Tree|`readTree()`|
|Tree → DTO|`treeToValue()`|
|DTO → JSON|`writeValueAsString()`|
|Merge JSON into DTO|`readerForUpdating()`|

---

## ✅ Final Rule (production rule)

> **All XML/JSON mapping belongs in backend**
> 
> **UI only consumes JSON**

---
```java
/*
========================================================
ONE FILE – ALL DTO + MAPPING + ANNOTATIONS + MAPPERS
(Spring Boot / Jackson / XML / JSON / Validation)
========================================================
*/

import com.fasterxml.jackson.annotation.*;
import com.fasterxml.jackson.databind.*;
import com.fasterxml.jackson.dataformat.xml.XmlMapper;

import jakarta.validation.constraints.*;
import jakarta.xml.bind.annotation.*;

import java.time.LocalDate;
import java.util.List;
import java.util.Map;

// ======================================================
// DTO (JSON + XML + Validation in ONE place)
// ======================================================

@XmlRootElement(name = "user")                         // XML root element
@JsonIgnoreProperties(ignoreUnknown = true)            // Ignore extra fields
@JsonInclude(JsonInclude.Include.NON_NULL)             // Exclude nulls
public class UserDTO {

    @JsonProperty("id")                                // JSON field name
    @XmlElement(name = "id")                           // XML field name
    @NotNull                                          // Validation
    public Long id;

    @JsonProperty("full_name")
    @JsonAlias({"name", "username"})                   // Accept legacy names
    @XmlElement(name = "full_name")
    @NotBlank
    public String name;

    @JsonIgnore                                        // Never serialized
    @XmlTransient
    public String password;

    @JsonFormat(pattern = "yyyy-MM-dd")                // Date format
    @XmlElement(name = "birth_date")
    public LocalDate birthDate;

    @XmlElementWrapper(name = "roles")                 // XML list wrapper
    @XmlElement(name = "role")
    public List<String> roles;

    // --------------------------------------------------
    // Immutable constructor support
    // --------------------------------------------------
    @JsonCreator
    public UserDTO(
            @JsonProperty("id") Long id,
            @JsonProperty("full_name") String name
    ) {
        this.id = id;
        this.name = name;
    }

    public UserDTO() {} // Required by Jackson / JAXB
}

// ======================================================
// ObjectMapper – ALL COMMON MAPPING CASES
// ======================================================

class MapperExamples {

    public static void main(String[] args) throws Exception {

        ObjectMapper jsonMapper = new ObjectMapper();
        XmlMapper xmlMapper = new XmlMapper();

        // Global config
        jsonMapper.configure(
                DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false
        );

        // ------------------------------------------------
        // JSON → DTO
        // ------------------------------------------------
        String json = """
        {
          "id": 1,
          "full_name": "Mohammed",
          "password": "secret",
          "birthDate": "1995-01-01"
        }
        """;

        UserDTO userFromJson = jsonMapper.readValue(json, UserDTO.class);

        // ------------------------------------------------
        // JSON → List<DTO>
        // ------------------------------------------------
        List<UserDTO> usersFromJson =
                jsonMapper.readValue(
                        "[" + json + "]",
                        new com.fasterxml.jackson.core.type.TypeReference<>() {}
                );

        // ------------------------------------------------
        // JSON → Map
        // ------------------------------------------------
        Map<String, Object> jsonMap =
                jsonMapper.readValue(json, Map.class);

        // ------------------------------------------------
        // Map → DTO
        // ------------------------------------------------
        UserDTO fromMap =
                jsonMapper.convertValue(jsonMap, UserDTO.class);

        // ------------------------------------------------
        // JSON → Tree (JsonNode)
        // ------------------------------------------------
        JsonNode node = jsonMapper.readTree(json);
        String extractedName = node.get("full_name").asText();

        // ------------------------------------------------
        // Tree → DTO
        // ------------------------------------------------
        UserDTO fromTree =
                jsonMapper.treeToValue(node, UserDTO.class);

        // ------------------------------------------------
        // DTO → JSON
        // ------------------------------------------------
        String backToJson =
                jsonMapper.writeValueAsString(fromTree);

        // ------------------------------------------------
        // Merge JSON into existing DTO
        // ------------------------------------------------
        UserDTO existing = new UserDTO();
        existing.id = 99L;

        jsonMapper.readerForUpdating(existing)
                .readValue("{\"full_name\":\"Updated\"}");

        // ------------------------------------------------
        // XML → DTO
        // ------------------------------------------------
        String xml = """
        <user>
          <id>5</id>
          <full_name>XML User</full_name>
          <birth_date>2000-02-02</birth_date>
        </user>
        """;

        UserDTO fromXml =
                xmlMapper.readValue(xml, UserDTO.class);

        // ------------------------------------------------
        // XML → JsonNode
        // ------------------------------------------------
        JsonNode xmlTree =
                xmlMapper.readTree(xml);

        // ------------------------------------------------
        // XML → DTO → JSON
        // ------------------------------------------------
        String xmlConvertedToJson =
                jsonMapper.writeValueAsString(fromXml);

        // ------------------------------------------------
        // Nested JSON → DTO
        // ------------------------------------------------
        String nestedJson = """
        {
          "user": {
            "id": 10,
            "full_name": "Nested User"
          }
        }
        """;

        JsonNode nestedNode =
                jsonMapper.readTree(nestedJson).get("user");

        UserDTO nestedUser =
                jsonMapper.treeToValue(nestedNode, UserDTO.class);
    }
}

/*
========================================================
MENTAL RULES (REMEMBER THESE)
========================================================

1. DTOs own serialization annotations
2. Entities should NOT have Jackson annotations
3. Backend converts XML → DTO → JSON
4. Frontend consumes JSON only
5. Use annotations for structure, ObjectMapper for behavior

========================================================
*/

```