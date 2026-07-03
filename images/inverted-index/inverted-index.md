# Inverted Index

An inverted index is an index data structure used in information retrieval systems and text databases to perform fast full-text searches. It stores a mapping from content keys (words or numbers) to their physical locations in a document or a set of documents, functioning like a hashmap that directs the query processor from a term to the specific documents containing it.

## Principles of Text Document Search

In large text search engines, scanning every document sequentially to find matching phrases is prohibitively slow. An inverted index resolves this bottleneck by pre-indexing every word across all documents, allowing the database engine to search by term rather than scanning raw file data.

## Features of Inverted Indexes

- **Accelerated Search**: Scans the index to immediately retrieve all documents containing the target term.
- **Fast Rebuild Speed**: Allows fast updates as new documents are introduced into the database.
- **Query Flexibility**: Supports complex boolean (AND, OR) and proximity search queries.
- **Compression Efficiency**: Enables high compression ratios using techniques like variable byte or delta encoding on posting lists.
- **Token Normalization**: Supports stemming and synonym mapping to match different forms of a root word.

## Steps to Build an Inverted Index

Building an inverted index involves three sequential steps:

### 1. Document Fetching and Stop Word Removal

The database fetches the document text and filters out high-frequency but low-information words (called stop words, such as "a", "the", "is", and "to") to minimize index size.

### 2. Stemming to Root Words

To group similar words, the engine strips prefixes and suffixes to extract the base root word (stemming). For example, words like "cats", "catty", and "catting" are mapped to the root word "cat" using standard algorithms like Porter's Stemmer.

### 3. Recording Document IDs

The engine records the mapping of the remaining unique terms to their corresponding document identifiers. If a term is already present in the index, its document list (posting list) is updated; otherwise, a new term entry is created.

- *Mini Example*:
- **ant** -&gt; doc1
- **demo** -&gt; doc2
- **world** -&gt; doc1, doc2

## Types of Inverted Indexes

Databases implement two main variants of inverted indexes:

### Record-Level Inverted Index

A record-level index mapping only links unique terms to the document IDs containing them, omitting word positions.

### Word-Level Inverted Index

A word-level index maps terms to document IDs and includes the exact word positions (offsets) within each document. This structure supports advanced proximity searches (e.g., finding words near each other) at the expense of storage.

- *Word-Level Case Study*: Consider three short text records:

1. "Mohit helps Akash"
2. "Akash assists Hemesh with database tables"
3. "Hemesh designs a database structure"

- *Word-Level Position Map*: We index the terms using the coordinate format `(DocumentID, WordIndex)`:
- mohit -&gt; (1, 1)
- helps -&gt; (1, 2)
- akash -&gt; (1, 3); (2, 1)
- assists -&gt; (2, 2)
- hemesh -&gt; (2, 3); (3, 1)
- with -&gt; (2, 4)
- database -&gt; (2, 5); (3, 3)
- tables -&gt; (2, 6)
- designs -&gt; (3, 2)
- a -&gt; (3, 4)
- structure -&gt; (3, 5)

## Analytical Case Study

We trace the index building process using two custom log documents:

- **Document 1**: "Mohit assigned a switch to Akash"
- **Document 2**: "Akash configured the new router for Hemesh"

### Unique Term Mapping

The query engine tokenizes and lowercases the terms, mapping them to their document lists:

- **mohit** -&gt; Document 1
- **assigned** -&gt; Document 1
- **a** -&gt; Document 1
- **switch** -&gt; Document 1
- **to** -&gt; Document 1
- **akash** -&gt; Document 1, Document 2
- **configured** -&gt; Document 2
- **the** -&gt; Document 2
- **new** -&gt; Document 2
- **router** -&gt; Document 2
- **for** -&gt; Document 2
- **hemesh** -&gt; Document 2

## Inverted Index Implementations

Below is the complete implementation of the document tokenization and index building algorithm in five languages. Each code block takes two documents, tokenizes and lowercases the terms, constructs the inverted index, and prints the resulting mapping.

```Java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        String doc1 = "mohit assigned a switch to akash";
        String doc2 = "akash configured the new router for hemesh";
        String[] tokens1 = doc1.toLowerCase().split("\\s+");
        String[] tokens2 = doc2.toLowerCase().split("\\s+");
        Set<String> uniqueTerms = new TreeSet<>();
        uniqueTerms.addAll(Arrays.asList(tokens1));
        uniqueTerms.addAll(Arrays.asList(tokens2));
        for (String term : uniqueTerms) {
            List<String> docs = new ArrayList<>();
            if (Arrays.asList(tokens1).contains(term)) {
                docs.add("Document 1");
            }
            if (Arrays.asList(tokens2).contains(term)) {
                docs.add("Document 2");
            }
            System.out.println(term + " -> " + String.join(", ", docs));
        }
    }
}
```
```C
#include <stdio.h>
#include <string.h>
#include <ctype.h>
#include <stdlib.h>

void to_lower(char* str) {
    for (int i = 0; str[i]; i++) {
        str[i] = tolower(str[i]);
    }
}

int split_string(const char* src, char dest[20][30]) {
    char temp[200];
    strcpy(temp, src);
    to_lower(temp);
    int count = 0;
    char* token = strtok(temp, " ");
    while (token != NULL) {
        strcpy(dest[count++], token);
        token = strtok(NULL, " ");
    }
    return count;
}

int contains(char tokens[20][30], int count, const char* word) {
    for (int i = 0; i < count; i++) {
        if (strcmp(tokens[i], word) == 0) return 1;
    }
    return 0;
}

int main() {
    const char* doc1 = "mohit assigned a switch to akash";
    const char* doc2 = "akash configured the new router for hemesh";
    char tokens1[20][30];
    char tokens2[20][30];
    int len1 = split_string(doc1, tokens1);
    int len2 = split_string(doc2, tokens2);
    char unique[40][30];
    int unique_count = 0;
    for (int i = 0; i < len1; i++) {
        int found = 0;
        for (int j = 0; j < unique_count; j++) {
            if (strcmp(unique[j], tokens1[i]) == 0) found = 1;
        }
        if (!found) strcpy(unique[unique_count++], tokens1[i]);
    }
    for (int i = 0; i < len2; i++) {
        int found = 0;
        for (int j = 0; j < unique_count; j++) {
            if (strcmp(unique[j], tokens2[i]) == 0) found = 1;
        }
        if (!found) strcpy(unique[unique_count++], tokens2[i]);
    }
    for (int i = 0; i < unique_count - 1; i++) {
        for (int j = 0; j < unique_count - i - 1; j++) {
            if (strcmp(unique[j], unique[j + 1]) > 0) {
                char temp[30];
                strcpy(temp, unique[j]);
                strcpy(unique[j], unique[j + 1]);
                strcpy(unique[j + 1], temp);
            }
        }
    }
    for (int i = 0; i < unique_count; i++) {
        int in_doc1 = contains(tokens1, len1, unique[i]);
        int in_doc2 = contains(tokens2, len2, unique[i]);
        printf("%s -> ", unique[i]);
        if (in_doc1 && in_doc2) {
            printf("Document 1, Document 2\n");
        } else if (in_doc1) {
            printf("Document 1\n");
        } else if (in_doc2) {
            printf("Document 2\n");
        }
    }
    return 0;
}
```
```Cpp
#include <iostream>
#include <string>
#include <vector>
#include <sstream>
#include <set>
#include <algorithm>

using namespace std;

vector<string> tokenize(const string& str) {
    vector<string> tokens;
    stringstream ss(str);
    string temp;
    while (ss >> temp) {
        transform(temp.begin(), temp.end(), temp.begin(), ::tolower);
        tokens.push_back(temp);
    }
    return tokens;
}

bool contains(const vector<string>& vec, const string& term) {
    return find(vec.begin(), vec.end(), term) != vec.end();
}

int main() {
    string doc1 = "mohit assigned a switch to akash";
    string doc2 = "akash configured the new router for hemesh";
    vector<string> tokens1 = tokenize(doc1);
    vector<string> tokens2 = tokenize(doc2);
    set<string> uniqueTerms;
    for (const auto& t : tokens1) uniqueTerms.insert(t);
    for (const auto& t : tokens2) uniqueTerms.insert(t);
    for (const auto& term : uniqueTerms) {
        vector<string> docs;
        if (contains(tokens1, term)) docs.push_back("Document 1");
        if (contains(tokens2, term)) docs.push_back("Document 2");
        cout << term << " -> ";
        for (size_t i = 0; i < docs.size(); ++i) {
            cout << docs[i] << (i + 1 < docs.size() ? ", " : "");
        }
        cout << endl;
    }
    return 0;
}
```
```Python
doc1 = "mohit assigned a switch to akash"
doc2 = "akash configured the new router for hemesh"
tokens1 = doc1.lower().split()
tokens2 = doc2.lower().split()
terms = sorted(list(set(tokens1 + tokens2)))
inverted_index = {}
for term in terms:
    docs = []
    if term in tokens1:
        docs.append("Document 1")
    if term in tokens2:
        docs.append("Document 2")
    inverted_index[term] = docs
for term, docs in inverted_index.items():
    print(term, "->", ", ".join(docs))
```
```JavaScript
const doc1 = "mohit assigned a switch to akash";
const doc2 = "akash configured the new router for hemesh";
const tokens1 = doc1.toLowerCase().split(/\s+/);
const tokens2 = doc2.toLowerCase().split(/\s+/);
const terms = Array.from(new Set([...tokens1, ...tokens2])).sort();
for (const term of terms) {
    const docs = [];
    if (tokens1.includes(term)) docs.push("Document 1");
    if (tokens2.includes(term)) docs.push("Document 2");
    console.log(`${term} -> ${docs.join(", ")}`);
}
```

## Performance Trade-Offs of Inverted Indexes

Implementing text indexes involves several performance trade-offs:

### Advantages of Inverted Indexes

- **Accelerated Full-Text Querying**: Allows search engines to immediately identify matching document sets.
- **Simplified Development**: The hashmap-based mapping is easy to design, implement, and extend.
- **Industry Standard**: It is the core data structure driving modern text retrieval engines and databases.

### Disadvantages of Inverted Indexes

- **Large Storage Consumption**: Storing unique terms, document lists, and positions requires high disk space.
- **High Maintenance Overhead**: Rebuilding or updating posting lists during write operations (inserts, updates, deletes) creates latency.
- **Unsorted Default Results**: Results are retrieved based on occurrence order in lists rather than relevance order, requiring an additional scoring pass (like TF-IDF).

## Comparison of Inverted Index Types

| Feature | Record-Level Inverted Index | Word-Level Inverted Index |
| --- | --- | --- |
| **Index Mapping Detail** | Maps terms to document identifiers only | Maps terms to document IDs and word offsets |
| **Proximity Search Support** | No (cannot identify relative word distances) | Yes (supports exact phrase and proximity lookups) |
| **Storage Footprint** | Low (stores compact list of document IDs) | High (requires storing offset integers for every word) |
| **Update Overhead** | Low | High (requires recalculating and rewriting offsets) |
| **Search Speed** | Fast for basic document checks | Slower for complex phrase position scans |

> **Key Insight**: The primary difference between record-level and word-level inverted indexes lies in query capabilities and storage footprints. While a record-level index is highly storage-efficient and fast for basic boolean document matching, a word-level index is mandatory for proximity and phrase queries because it records the exact offset position of each word within the documents.

# Summary

An inverted index is a hashmap-like data structure designed to support high-speed full-text searches in document retrieval engines. By tokenizing text, removing stop words, stemming root words, and mapping unique terms to their document references, the index bypasses linear table scans. Systems implement record-level indexing for basic document lookups or word-level indexing to record exact word offsets for complex phrase searches. Relational databases evaluate inverted indexing against B+ Trees to optimize search latency for unstructured text fields.




