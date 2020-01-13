# HTML Similarity

This package provides a set of functions to measure the similarity between web pages.

## Install

The quick way::

    go get -u github.com/cckuailong/simHtml

## How it works?

### Structural Similarity

Uses sequence comparison of the html tags to compute the similarity.

We not implement the similarity based on tree edit distance because it is slower than sequence comparison.


### Style Similarity

Extracts css classes of each html document and calculates the jaccard similarity of the sets of classes.


### Joint Similarity (Structural Similarity and Style Similarity)

The joint similarity metric is calculated as::

    k * structural_similarity(document_1, document_2) + (1 - k) * style_similarity(document_1, document_2)

All the similarity metrics takes values between 0 and 1.

### Recommendations for joint similarity

Using `k=0.3` give use better results. The style similarity gives more information about the similarity rather than the structural similarity.

## Examples

    In [1]: 1.html's content is
     '''
     <html>
        <h1 class="title">First Document</h1>
        <ul class="menu">
            <li class="active">Documents</li>
            <li>Extra</li>
        </ul>
     </html>
    '''

    In [2]: 2.html's content is
    '''
    <html>
        <h1 class="title">Second document Document</h1>
        <ul class="menu">
            <li class="active">Extra Documents</li>
        </ul>
    </html>
    '''

    In [3] import "github.com/cckuailong/simHtml/simHtml"

    In [4]: simHtml.GetSimRate("./1.html", "./2.html")
    Out[4]: 0.9545454545454546

### References

- html-similarity <https://github.com/matiskay/html-similarity>