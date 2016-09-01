# Entropy
This script provides a way to otherize a categorical feature based on the entropy with respect to the target. It is provided as a ipython notebook (2.7) that you should run with jupyter.

## Otherization
When writing datascience scripts, you sometimes face categorical features. As these features cannot be used "as is" by the learning algorithms, you often dummify these features in as many columns as categories the feature represents. But if the feature cardinality is high, you cannot proceed this way without getting way too much columns.

A solution is to otherize the feature: keep the main categories and put them in separate columns, and put the remaining categories all together in a unique "others" column.

## Entropy-based otherization
Often, otherization is done with respect to cardinality: we keep the categories the most represented. This can work, but we wanted to provide an other way to do this, in a more thoughtful way.

Basically, the script computes the entropy of the feature with respect to the target (which must be a class-like target, no regression), considering that all categories are "others". Then, it extracts one category, and compute the new entropy with one category separated from the "others". We do this on all the categories, and select the category which corresponds to the lowest entropy.
This category is kept apart, and we select a second one with the same process

## Limits
This way of proceeding values the direct correlation/signal between the categories and the target. It does not help with hidden signal that would be highlighted if a category was mixed with another feature by a non-linear algorithm.

Moreover, categorical features seem to be treated more efficiently by xgboost when simply label encoded. XGBoost then finds himself the splits to do on the feature.

However, this script can still be useful : it is of great help when explaining features with non-datascientist people, and helps to understand the data. Just keep in mind that some algorithms *may* do better.

