{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "authorship_tag": "ABX9TyOxBMTGzIjqzxAUkESTqD/h",
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/13D4C/Data_analysis_Iphone_2021/blob/main/Data_analysis_Iphone_2021.ipynb\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "qqSSB_KIoqjJ"
      },
      "outputs": [],
      "source": [
        "import pandas as pd\n",
        "import numpy as np\n",
        "import matplotlib.pyplot as plt\n",
        "import seaborn as sns\n",
        "import plotly.express as px\n",
        "import plotly.graph_objects as go\n",
        "import matplotlib.pyplot as plt\n",
        "from sklearn.linear_model import LinearRegression"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "df = pd.read_csv(\"/content/apple_products.csv\")"
      ],
      "metadata": {
        "id": "K3RYd0gQoyZX"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "df.head()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 414
        },
        "id": "VmMzoy-5oycL",
        "outputId": "db62e53a-411f-4429-d96e-d4c2106444a2"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "                               Product Name  \\\n",
              "0         APPLE iPhone 8 Plus (Gold, 64 GB)   \n",
              "1  APPLE iPhone 8 Plus (Space Grey, 256 GB)   \n",
              "2      APPLE iPhone 8 Plus (Silver, 256 GB)   \n",
              "3           APPLE iPhone 8 (Silver, 256 GB)   \n",
              "4             APPLE iPhone 8 (Gold, 256 GB)   \n",
              "\n",
              "                                         Product URL  Brand  Sale Price  \\\n",
              "0  https://www.flipkart.com/apple-iphone-8-plus-g...  Apple       49900   \n",
              "1  https://www.flipkart.com/apple-iphone-8-plus-s...  Apple       84900   \n",
              "2  https://www.flipkart.com/apple-iphone-8-plus-s...  Apple       84900   \n",
              "3  https://www.flipkart.com/apple-iphone-8-silver...  Apple       77000   \n",
              "4  https://www.flipkart.com/apple-iphone-8-gold-2...  Apple       77000   \n",
              "\n",
              "     Mrp  Discount Percentage  Number Of Ratings  Number Of Reviews  \\\n",
              "0  49900                    0               3431                356   \n",
              "1  84900                    0               3431                356   \n",
              "2  84900                    0               3431                356   \n",
              "3  77000                    0              11202                794   \n",
              "4  77000                    0              11202                794   \n",
              "\n",
              "                Upc  Star Rating   Ram  \n",
              "0  MOBEXRGV7EHHTGUH          4.6  2 GB  \n",
              "1  MOBEXRGVAC6TJT4F          4.6  2 GB  \n",
              "2  MOBEXRGVGETABXWZ          4.6  2 GB  \n",
              "3  MOBEXRGVMZWUHCBA          4.5  2 GB  \n",
              "4  MOBEXRGVPK7PFEJZ          4.5  2 GB  "
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-221bf7bf-c700-4d3a-8f2f-9e5c3a71e20e\" class=\"colab-df-container\">\n",
              "    <div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>Product Name</th>\n",
              "      <th>Product URL</th>\n",
              "      <th>Brand</th>\n",
              "      <th>Sale Price</th>\n",
              "      <th>Mrp</th>\n",
              "      <th>Discount Percentage</th>\n",
              "      <th>Number Of Ratings</th>\n",
              "      <th>Number Of Reviews</th>\n",
              "      <th>Upc</th>\n",
              "      <th>Star Rating</th>\n",
              "      <th>Ram</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>APPLE iPhone 8 Plus (Gold, 64 GB)</td>\n",
              "      <td>https://www.flipkart.com/apple-iphone-8-plus-g...</td>\n",
              "      <td>Apple</td>\n",
              "      <td>49900</td>\n",
              "      <td>49900</td>\n",
              "      <td>0</td>\n",
              "      <td>3431</td>\n",
              "      <td>356</td>\n",
              "      <td>MOBEXRGV7EHHTGUH</td>\n",
              "      <td>4.6</td>\n",
              "      <td>2 GB</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>APPLE iPhone 8 Plus (Space Grey, 256 GB)</td>\n",
              "      <td>https://www.flipkart.com/apple-iphone-8-plus-s...</td>\n",
              "      <td>Apple</td>\n",
              "      <td>84900</td>\n",
              "      <td>84900</td>\n",
              "      <td>0</td>\n",
              "      <td>3431</td>\n",
              "      <td>356</td>\n",
              "      <td>MOBEXRGVAC6TJT4F</td>\n",
              "      <td>4.6</td>\n",
              "      <td>2 GB</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>APPLE iPhone 8 Plus (Silver, 256 GB)</td>\n",
              "      <td>https://www.flipkart.com/apple-iphone-8-plus-s...</td>\n",
              "      <td>Apple</td>\n",
              "      <td>84900</td>\n",
              "      <td>84900</td>\n",
              "      <td>0</td>\n",
              "      <td>3431</td>\n",
              "      <td>356</td>\n",
              "      <td>MOBEXRGVGETABXWZ</td>\n",
              "      <td>4.6</td>\n",
              "      <td>2 GB</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>APPLE iPhone 8 (Silver, 256 GB)</td>\n",
              "      <td>https://www.flipkart.com/apple-iphone-8-silver...</td>\n",
              "      <td>Apple</td>\n",
              "      <td>77000</td>\n",
              "      <td>77000</td>\n",
              "      <td>0</td>\n",
              "      <td>11202</td>\n",
              "      <td>794</td>\n",
              "      <td>MOBEXRGVMZWUHCBA</td>\n",
              "      <td>4.5</td>\n",
              "      <td>2 GB</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>APPLE iPhone 8 (Gold, 256 GB)</td>\n",
              "      <td>https://www.flipkart.com/apple-iphone-8-gold-2...</td>\n",
              "      <td>Apple</td>\n",
              "      <td>77000</td>\n",
              "      <td>77000</td>\n",
              "      <td>0</td>\n",
              "      <td>11202</td>\n",
              "      <td>794</td>\n",
              "      <td>MOBEXRGVPK7PFEJZ</td>\n",
              "      <td>4.5</td>\n",
              "      <td>2 GB</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "    <div class=\"colab-df-buttons\">\n",
              "\n",
              "  <div class=\"colab-df-container\">\n",
              "    <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-221bf7bf-c700-4d3a-8f2f-9e5c3a71e20e')\"\n",
              "            title=\"Convert this dataframe to an interactive table.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\" viewBox=\"0 -960 960 960\">\n",
              "    <path d=\"M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z\"/>\n",
              "  </svg>\n",
              "    </button>\n",
              "\n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    .colab-df-buttons div {\n",
              "      margin-bottom: 4px;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "    <script>\n",
              "      const buttonEl =\n",
              "        document.querySelector('#df-221bf7bf-c700-4d3a-8f2f-9e5c3a71e20e button.colab-df-convert');\n",
              "      buttonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "      async function convertToInteractive(key) {\n",
              "        const element = document.querySelector('#df-221bf7bf-c700-4d3a-8f2f-9e5c3a71e20e');\n",
              "        const dataTable =\n",
              "          await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                    [key], {});\n",
              "        if (!dataTable) return;\n",
              "\n",
              "        const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "          '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "          + ' to learn more about interactive tables.';\n",
              "        element.innerHTML = '';\n",
              "        dataTable['output_type'] = 'display_data';\n",
              "        await google.colab.output.renderOutput(dataTable, element);\n",
              "        const docLink = document.createElement('div');\n",
              "        docLink.innerHTML = docLinkHtml;\n",
              "        element.appendChild(docLink);\n",
              "      }\n",
              "    </script>\n",
              "  </div>\n",
              "\n",
              "\n",
              "<div id=\"df-c15f4a34-9d17-4754-a327-f27fbc93a609\">\n",
              "  <button class=\"colab-df-quickchart\" onclick=\"quickchart('df-c15f4a34-9d17-4754-a327-f27fbc93a609')\"\n",
              "            title=\"Suggest charts.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "<svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "     width=\"24px\">\n",
              "    <g>\n",
              "        <path d=\"M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z\"/>\n",
              "    </g>\n",
              "</svg>\n",
              "  </button>\n",
              "\n",
              "<style>\n",
              "  .colab-df-quickchart {\n",
              "      --bg-color: #E8F0FE;\n",
              "      --fill-color: #1967D2;\n",
              "      --hover-bg-color: #E2EBFA;\n",
              "      --hover-fill-color: #174EA6;\n",
              "      --disabled-fill-color: #AAA;\n",
              "      --disabled-bg-color: #DDD;\n",
              "  }\n",
              "\n",
              "  [theme=dark] .colab-df-quickchart {\n",
              "      --bg-color: #3B4455;\n",
              "      --fill-color: #D2E3FC;\n",
              "      --hover-bg-color: #434B5C;\n",
              "      --hover-fill-color: #FFFFFF;\n",
              "      --disabled-bg-color: #3B4455;\n",
              "      --disabled-fill-color: #666;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart {\n",
              "    background-color: var(--bg-color);\n",
              "    border: none;\n",
              "    border-radius: 50%;\n",
              "    cursor: pointer;\n",
              "    display: none;\n",
              "    fill: var(--fill-color);\n",
              "    height: 32px;\n",
              "    padding: 0;\n",
              "    width: 32px;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart:hover {\n",
              "    background-color: var(--hover-bg-color);\n",
              "    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "    fill: var(--button-hover-fill-color);\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart-complete:disabled,\n",
              "  .colab-df-quickchart-complete:disabled:hover {\n",
              "    background-color: var(--disabled-bg-color);\n",
              "    fill: var(--disabled-fill-color);\n",
              "    box-shadow: none;\n",
              "  }\n",
              "\n",
              "  .colab-df-spinner {\n",
              "    border: 2px solid var(--fill-color);\n",
              "    border-color: transparent;\n",
              "    border-bottom-color: var(--fill-color);\n",
              "    animation:\n",
              "      spin 1s steps(1) infinite;\n",
              "  }\n",
              "\n",
              "  @keyframes spin {\n",
              "    0% {\n",
              "      border-color: transparent;\n",
              "      border-bottom-color: var(--fill-color);\n",
              "      border-left-color: var(--fill-color);\n",
              "    }\n",
              "    20% {\n",
              "      border-color: transparent;\n",
              "      border-left-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "    }\n",
              "    30% {\n",
              "      border-color: transparent;\n",
              "      border-left-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "      border-right-color: var(--fill-color);\n",
              "    }\n",
              "    40% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "    }\n",
              "    60% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "    }\n",
              "    80% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "      border-bottom-color: var(--fill-color);\n",
              "    }\n",
              "    90% {\n",
              "      border-color: transparent;\n",
              "      border-bottom-color: var(--fill-color);\n",
              "    }\n",
              "  }\n",
              "</style>\n",
              "\n",
              "  <script>\n",
              "    async function quickchart(key) {\n",
              "      const quickchartButtonEl =\n",
              "        document.querySelector('#' + key + ' button');\n",
              "      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.\n",
              "      quickchartButtonEl.classList.add('colab-df-spinner');\n",
              "      try {\n",
              "        const charts = await google.colab.kernel.invokeFunction(\n",
              "            'suggestCharts', [key], {});\n",
              "      } catch (error) {\n",
              "        console.error('Error during call to suggestCharts:', error);\n",
              "      }\n",
              "      quickchartButtonEl.classList.remove('colab-df-spinner');\n",
              "      quickchartButtonEl.classList.add('colab-df-quickchart-complete');\n",
              "    }\n",
              "    (() => {\n",
              "      let quickchartButtonEl =\n",
              "        document.querySelector('#df-c15f4a34-9d17-4754-a327-f27fbc93a609 button');\n",
              "      quickchartButtonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "    })();\n",
              "  </script>\n",
              "</div>\n",
              "    </div>\n",
              "  </div>\n"
            ]
          },
          "metadata": {},
          "execution_count": 3
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "df.describe()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 300
        },
        "id": "5qru6tPSoyfF",
        "outputId": "9d4bb189-2c62-4e98-cb9f-e25f4ef8d0da"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "          Sale Price            Mrp  Discount Percentage  Number Of Ratings  \\\n",
              "count      62.000000      62.000000            62.000000          62.000000   \n",
              "mean    80073.887097   88058.064516             9.951613       22420.403226   \n",
              "std     34310.446132   34728.825597             7.608079       33768.589550   \n",
              "min     29999.000000   39900.000000             0.000000         542.000000   \n",
              "25%     49900.000000   54900.000000             6.000000         740.000000   \n",
              "50%     75900.000000   79900.000000            10.000000        2101.000000   \n",
              "75%    117100.000000  120950.000000            14.000000       43470.000000   \n",
              "max    140900.000000  149900.000000            29.000000       95909.000000   \n",
              "\n",
              "       Number Of Reviews  Star Rating  \n",
              "count          62.000000    62.000000  \n",
              "mean         1861.677419     4.575806  \n",
              "std          2855.883830     0.059190  \n",
              "min            42.000000     4.500000  \n",
              "25%            64.000000     4.500000  \n",
              "50%           180.000000     4.600000  \n",
              "75%          3331.000000     4.600000  \n",
              "max          8161.000000     4.700000  "
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-a796d840-ff2b-492d-b989-2ffd615383a0\" class=\"colab-df-container\">\n",
              "    <div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>Sale Price</th>\n",
              "      <th>Mrp</th>\n",
              "      <th>Discount Percentage</th>\n",
              "      <th>Number Of Ratings</th>\n",
              "      <th>Number Of Reviews</th>\n",
              "      <th>Star Rating</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>count</th>\n",
              "      <td>62.000000</td>\n",
              "      <td>62.000000</td>\n",
              "      <td>62.000000</td>\n",
              "      <td>62.000000</td>\n",
              "      <td>62.000000</td>\n",
              "      <td>62.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>mean</th>\n",
              "      <td>80073.887097</td>\n",
              "      <td>88058.064516</td>\n",
              "      <td>9.951613</td>\n",
              "      <td>22420.403226</td>\n",
              "      <td>1861.677419</td>\n",
              "      <td>4.575806</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>std</th>\n",
              "      <td>34310.446132</td>\n",
              "      <td>34728.825597</td>\n",
              "      <td>7.608079</td>\n",
              "      <td>33768.589550</td>\n",
              "      <td>2855.883830</td>\n",
              "      <td>0.059190</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>min</th>\n",
              "      <td>29999.000000</td>\n",
              "      <td>39900.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>542.000000</td>\n",
              "      <td>42.000000</td>\n",
              "      <td>4.500000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>25%</th>\n",
              "      <td>49900.000000</td>\n",
              "      <td>54900.000000</td>\n",
              "      <td>6.000000</td>\n",
              "      <td>740.000000</td>\n",
              "      <td>64.000000</td>\n",
              "      <td>4.500000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>50%</th>\n",
              "      <td>75900.000000</td>\n",
              "      <td>79900.000000</td>\n",
              "      <td>10.000000</td>\n",
              "      <td>2101.000000</td>\n",
              "      <td>180.000000</td>\n",
              "      <td>4.600000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>75%</th>\n",
              "      <td>117100.000000</td>\n",
              "      <td>120950.000000</td>\n",
              "      <td>14.000000</td>\n",
              "      <td>43470.000000</td>\n",
              "      <td>3331.000000</td>\n",
              "      <td>4.600000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>max</th>\n",
              "      <td>140900.000000</td>\n",
              "      <td>149900.000000</td>\n",
              "      <td>29.000000</td>\n",
              "      <td>95909.000000</td>\n",
              "      <td>8161.000000</td>\n",
              "      <td>4.700000</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "    <div class=\"colab-df-buttons\">\n",
              "\n",
              "  <div class=\"colab-df-container\">\n",
              "    <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-a796d840-ff2b-492d-b989-2ffd615383a0')\"\n",
              "            title=\"Convert this dataframe to an interactive table.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\" viewBox=\"0 -960 960 960\">\n",
              "    <path d=\"M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z\"/>\n",
              "  </svg>\n",
              "    </button>\n",
              "\n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    .colab-df-buttons div {\n",
              "      margin-bottom: 4px;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "    <script>\n",
              "      const buttonEl =\n",
              "        document.querySelector('#df-a796d840-ff2b-492d-b989-2ffd615383a0 button.colab-df-convert');\n",
              "      buttonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "      async function convertToInteractive(key) {\n",
              "        const element = document.querySelector('#df-a796d840-ff2b-492d-b989-2ffd615383a0');\n",
              "        const dataTable =\n",
              "          await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                    [key], {});\n",
              "        if (!dataTable) return;\n",
              "\n",
              "        const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "          '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "          + ' to learn more about interactive tables.';\n",
              "        element.innerHTML = '';\n",
              "        dataTable['output_type'] = 'display_data';\n",
              "        await google.colab.output.renderOutput(dataTable, element);\n",
              "        const docLink = document.createElement('div');\n",
              "        docLink.innerHTML = docLinkHtml;\n",
              "        element.appendChild(docLink);\n",
              "      }\n",
              "    </script>\n",
              "  </div>\n",
              "\n",
              "\n",
              "<div id=\"df-9fc534ba-a877-450f-9a78-af5eb22a6730\">\n",
              "  <button class=\"colab-df-quickchart\" onclick=\"quickchart('df-9fc534ba-a877-450f-9a78-af5eb22a6730')\"\n",
              "            title=\"Suggest charts.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "<svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "     width=\"24px\">\n",
              "    <g>\n",
              "        <path d=\"M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z\"/>\n",
              "    </g>\n",
              "</svg>\n",
              "  </button>\n",
              "\n",
              "<style>\n",
              "  .colab-df-quickchart {\n",
              "      --bg-color: #E8F0FE;\n",
              "      --fill-color: #1967D2;\n",
              "      --hover-bg-color: #E2EBFA;\n",
              "      --hover-fill-color: #174EA6;\n",
              "      --disabled-fill-color: #AAA;\n",
              "      --disabled-bg-color: #DDD;\n",
              "  }\n",
              "\n",
              "  [theme=dark] .colab-df-quickchart {\n",
              "      --bg-color: #3B4455;\n",
              "      --fill-color: #D2E3FC;\n",
              "      --hover-bg-color: #434B5C;\n",
              "      --hover-fill-color: #FFFFFF;\n",
              "      --disabled-bg-color: #3B4455;\n",
              "      --disabled-fill-color: #666;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart {\n",
              "    background-color: var(--bg-color);\n",
              "    border: none;\n",
              "    border-radius: 50%;\n",
              "    cursor: pointer;\n",
              "    display: none;\n",
              "    fill: var(--fill-color);\n",
              "    height: 32px;\n",
              "    padding: 0;\n",
              "    width: 32px;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart:hover {\n",
              "    background-color: var(--hover-bg-color);\n",
              "    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "    fill: var(--button-hover-fill-color);\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart-complete:disabled,\n",
              "  .colab-df-quickchart-complete:disabled:hover {\n",
              "    background-color: var(--disabled-bg-color);\n",
              "    fill: var(--disabled-fill-color);\n",
              "    box-shadow: none;\n",
              "  }\n",
              "\n",
              "  .colab-df-spinner {\n",
              "    border: 2px solid var(--fill-color);\n",
              "    border-color: transparent;\n",
              "    border-bottom-color: var(--fill-color);\n",
              "    animation:\n",
              "      spin 1s steps(1) infinite;\n",
              "  }\n",
              "\n",
              "  @keyframes spin {\n",
              "    0% {\n",
              "      border-color: transparent;\n",
              "      border-bottom-color: var(--fill-color);\n",
              "      border-left-color: var(--fill-color);\n",
              "    }\n",
              "    20% {\n",
              "      border-color: transparent;\n",
              "      border-left-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "    }\n",
              "    30% {\n",
              "      border-color: transparent;\n",
              "      border-left-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "      border-right-color: var(--fill-color);\n",
              "    }\n",
              "    40% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "    }\n",
              "    60% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "    }\n",
              "    80% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "      border-bottom-color: var(--fill-color);\n",
              "    }\n",
              "    90% {\n",
              "      border-color: transparent;\n",
              "      border-bottom-color: var(--fill-color);\n",
              "    }\n",
              "  }\n",
              "</style>\n",
              "\n",
              "  <script>\n",
              "    async function quickchart(key) {\n",
              "      const quickchartButtonEl =\n",
              "        document.querySelector('#' + key + ' button');\n",
              "      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.\n",
              "      quickchartButtonEl.classList.add('colab-df-spinner');\n",
              "      try {\n",
              "        const charts = await google.colab.kernel.invokeFunction(\n",
              "            'suggestCharts', [key], {});\n",
              "      } catch (error) {\n",
              "        console.error('Error during call to suggestCharts:', error);\n",
              "      }\n",
              "      quickchartButtonEl.classList.remove('colab-df-spinner');\n",
              "      quickchartButtonEl.classList.add('colab-df-quickchart-complete');\n",
              "    }\n",
              "    (() => {\n",
              "      let quickchartButtonEl =\n",
              "        document.querySelector('#df-9fc534ba-a877-450f-9a78-af5eb22a6730 button');\n",
              "      quickchartButtonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "    })();\n",
              "  </script>\n",
              "</div>\n",
              "    </div>\n",
              "  </div>\n"
            ]
          },
          "metadata": {},
          "execution_count": 4
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "iphone_8 = df.iloc[0:7]"
      ],
      "metadata": {
        "id": "h5Hxny0moyhx"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "counts = iphone_8[\"Number Of Ratings\"]\n",
        "fig = px.bar(iphone_8, x='Product Name', y = counts,)\n",
        "\n",
        "fig.show()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 542
        },
        "id": "adAgFj2Aoyke",
        "outputId": "0ed169de-906d-4a93-eac4-90063d56f38e"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/html": [
              "<html>\n",
              "<head><meta charset=\"utf-8\" /></head>\n",
              "<body>\n",
              "    <div>            <script src=\"https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG\"></script><script type=\"text/javascript\">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: \"STIX-Web\"}});}</script>                <script type=\"text/javascript\">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>\n",
              "        <script charset=\"utf-8\" src=\"https://cdn.plot.ly/plotly-2.24.1.min.js\"></script>                <div id=\"f9d3c444-1dee-4558-a608-f574383b2a0f\" class=\"plotly-graph-div\" style=\"height:525px; width:100%;\"></div>            <script type=\"text/javascript\">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById(\"f9d3c444-1dee-4558-a608-f574383b2a0f\")) {                    Plotly.newPlot(                        \"f9d3c444-1dee-4558-a608-f574383b2a0f\",                        [{\"alignmentgroup\":\"True\",\"hovertemplate\":\"Product Name=%{x}\\u003cbr\\u003eNumber Of Ratings=%{y}\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"pattern\":{\"shape\":\"\"}},\"name\":\"\",\"offsetgroup\":\"\",\"orientation\":\"v\",\"showlegend\":false,\"textposition\":\"auto\",\"x\":[\"APPLE iPhone 8 Plus (Gold, 64 GB)\",\"APPLE iPhone 8 Plus (Space Grey, 256 GB)\",\"APPLE iPhone 8 Plus (Silver, 256 GB)\",\"APPLE iPhone 8 (Silver, 256 GB)\",\"APPLE iPhone 8 (Gold, 256 GB)\",\"APPLE iPhone 8 Plus (Silver, 64 GB)\",\"APPLE iPhone 8 Plus (Space Grey, 64 GB)\"],\"xaxis\":\"x\",\"y\":[3431,3431,3431,11202,11202,3431,3431],\"yaxis\":\"y\",\"type\":\"bar\"}],                        {\"template\":{\"data\":{\"histogram2dcontour\":[{\"type\":\"histogram2dcontour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"choropleth\":[{\"type\":\"choropleth\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"histogram2d\":[{\"type\":\"histogram2d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmap\":[{\"type\":\"heatmap\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmapgl\":[{\"type\":\"heatmapgl\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"contourcarpet\":[{\"type\":\"contourcarpet\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"contour\":[{\"type\":\"contour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"surface\":[{\"type\":\"surface\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"mesh3d\":[{\"type\":\"mesh3d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"scatter\":[{\"fillpattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2},\"type\":\"scatter\"}],\"parcoords\":[{\"type\":\"parcoords\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolargl\":[{\"type\":\"scatterpolargl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"bar\":[{\"error_x\":{\"color\":\"#2a3f5f\"},\"error_y\":{\"color\":\"#2a3f5f\"},\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"bar\"}],\"scattergeo\":[{\"type\":\"scattergeo\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolar\":[{\"type\":\"scatterpolar\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"histogram\":[{\"marker\":{\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"histogram\"}],\"scattergl\":[{\"type\":\"scattergl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatter3d\":[{\"type\":\"scatter3d\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattermapbox\":[{\"type\":\"scattermapbox\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterternary\":[{\"type\":\"scatterternary\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattercarpet\":[{\"type\":\"scattercarpet\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"carpet\":[{\"aaxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"baxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"type\":\"carpet\"}],\"table\":[{\"cells\":{\"fill\":{\"color\":\"#EBF0F8\"},\"line\":{\"color\":\"white\"}},\"header\":{\"fill\":{\"color\":\"#C8D4E3\"},\"line\":{\"color\":\"white\"}},\"type\":\"table\"}],\"barpolar\":[{\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"barpolar\"}],\"pie\":[{\"automargin\":true,\"type\":\"pie\"}]},\"layout\":{\"autotypenumbers\":\"strict\",\"colorway\":[\"#636efa\",\"#EF553B\",\"#00cc96\",\"#ab63fa\",\"#FFA15A\",\"#19d3f3\",\"#FF6692\",\"#B6E880\",\"#FF97FF\",\"#FECB52\"],\"font\":{\"color\":\"#2a3f5f\"},\"hovermode\":\"closest\",\"hoverlabel\":{\"align\":\"left\"},\"paper_bgcolor\":\"white\",\"plot_bgcolor\":\"#E5ECF6\",\"polar\":{\"bgcolor\":\"#E5ECF6\",\"angularaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"radialaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"ternary\":{\"bgcolor\":\"#E5ECF6\",\"aaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"baxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"caxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"coloraxis\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"colorscale\":{\"sequential\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"sequentialminus\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"diverging\":[[0,\"#8e0152\"],[0.1,\"#c51b7d\"],[0.2,\"#de77ae\"],[0.3,\"#f1b6da\"],[0.4,\"#fde0ef\"],[0.5,\"#f7f7f7\"],[0.6,\"#e6f5d0\"],[0.7,\"#b8e186\"],[0.8,\"#7fbc41\"],[0.9,\"#4d9221\"],[1,\"#276419\"]]},\"xaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"yaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"scene\":{\"xaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"yaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"zaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2}},\"shapedefaults\":{\"line\":{\"color\":\"#2a3f5f\"}},\"annotationdefaults\":{\"arrowcolor\":\"#2a3f5f\",\"arrowhead\":0,\"arrowwidth\":1},\"geo\":{\"bgcolor\":\"white\",\"landcolor\":\"#E5ECF6\",\"subunitcolor\":\"white\",\"showland\":true,\"showlakes\":true,\"lakecolor\":\"white\"},\"title\":{\"x\":0.05},\"mapbox\":{\"style\":\"light\"}}},\"xaxis\":{\"anchor\":\"y\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Product Name\"}},\"yaxis\":{\"anchor\":\"x\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Number Of Ratings\"}},\"legend\":{\"tracegroupgap\":0},\"margin\":{\"t\":60},\"barmode\":\"relative\"},                        {\"responsive\": true}                    ).then(function(){\n",
              "                            \n",
              "var gd = document.getElementById('f9d3c444-1dee-4558-a608-f574383b2a0f');\n",
              "var x = new MutationObserver(function (mutations, observer) {{\n",
              "        var display = window.getComputedStyle(gd).display;\n",
              "        if (!display || display === 'none') {{\n",
              "            console.log([gd, 'removed!']);\n",
              "            Plotly.purge(gd);\n",
              "            observer.disconnect();\n",
              "        }}\n",
              "}});\n",
              "\n",
              "// Listen for the removal of the full notebook cells\n",
              "var notebookContainer = gd.closest('#notebook-container');\n",
              "if (notebookContainer) {{\n",
              "    x.observe(notebookContainer, {childList: true});\n",
              "}}\n",
              "\n",
              "// Listen for the clearing of the current output cell\n",
              "var outputEl = gd.closest('.output');\n",
              "if (outputEl) {{\n",
              "    x.observe(outputEl, {childList: true});\n",
              "}}\n",
              "\n",
              "                        })                };                            </script>        </div>\n",
              "</body>\n",
              "</html>"
            ]
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "Iphone 8 gold and silver Number Of Ratings พอๆกันหมด"
      ],
      "metadata": {
        "id": "BpMt7Daap8d4"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "figure = px.scatter(data_frame = iphone_8, x=\"Number Of Ratings\",\n",
        "                    y=\"Sale Price\", size=\"Discount Percentage\",\n",
        "                    trendline=\"ols\",\n",
        "                    title=\"Relationship between Sale Price and Number of Ratings of iPhones 8\")\n",
        "figure.show()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 542
        },
        "id": "w03oByiVrvRd",
        "outputId": "a7fe670b-5a9e-48a0-8166-7c7cb182e44b"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/html": [
              "<html>\n",
              "<head><meta charset=\"utf-8\" /></head>\n",
              "<body>\n",
              "    <div>            <script src=\"https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG\"></script><script type=\"text/javascript\">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: \"STIX-Web\"}});}</script>                <script type=\"text/javascript\">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>\n",
              "        <script charset=\"utf-8\" src=\"https://cdn.plot.ly/plotly-2.24.1.min.js\"></script>                <div id=\"d775a701-b656-4935-a115-0f55d701e9d8\" class=\"plotly-graph-div\" style=\"height:525px; width:100%;\"></div>            <script type=\"text/javascript\">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById(\"d775a701-b656-4935-a115-0f55d701e9d8\")) {                    Plotly.newPlot(                        \"d775a701-b656-4935-a115-0f55d701e9d8\",                        [{\"hovertemplate\":\"Number Of Ratings=%{x}\\u003cbr\\u003eSale Price=%{y}\\u003cbr\\u003eDiscount Percentage=%{marker.size}\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"size\":[0,0,0,0,0,0,0],\"sizemode\":\"area\",\"sizeref\":0.0,\"symbol\":\"circle\"},\"mode\":\"markers\",\"name\":\"\",\"orientation\":\"v\",\"showlegend\":false,\"x\":[3431,3431,3431,11202,11202,3431,3431],\"xaxis\":\"x\",\"y\":[49900,84900,84900,77000,77000,49900,49900],\"yaxis\":\"y\",\"type\":\"scatter\"},{\"hovertemplate\":\"\\u003cb\\u003eOLS trendline\\u003c\\u002fb\\u003e\\u003cbr\\u003eSale Price = 1.68575 * Number Of Ratings + 58116.2\\u003cbr\\u003eR\\u003csup\\u003e2\\u003c\\u002fsup\\u003e=0.142936\\u003cbr\\u003e\\u003cbr\\u003eNumber Of Ratings=%{x}\\u003cbr\\u003eSale Price=%{y} \\u003cb\\u003e(trend)\\u003c\\u002fb\\u003e\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"symbol\":\"circle\"},\"mode\":\"lines\",\"name\":\"\",\"showlegend\":false,\"x\":[3431,3431,3431,3431,3431,11202,11202],\"xaxis\":\"x\",\"y\":[63900.0,63900.0,63900.0,63900.0,63900.0,77000.0,77000.0],\"yaxis\":\"y\",\"type\":\"scatter\"}],                        {\"template\":{\"data\":{\"histogram2dcontour\":[{\"type\":\"histogram2dcontour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"choropleth\":[{\"type\":\"choropleth\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"histogram2d\":[{\"type\":\"histogram2d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmap\":[{\"type\":\"heatmap\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmapgl\":[{\"type\":\"heatmapgl\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"contourcarpet\":[{\"type\":\"contourcarpet\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"contour\":[{\"type\":\"contour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"surface\":[{\"type\":\"surface\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"mesh3d\":[{\"type\":\"mesh3d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"scatter\":[{\"fillpattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2},\"type\":\"scatter\"}],\"parcoords\":[{\"type\":\"parcoords\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolargl\":[{\"type\":\"scatterpolargl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"bar\":[{\"error_x\":{\"color\":\"#2a3f5f\"},\"error_y\":{\"color\":\"#2a3f5f\"},\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"bar\"}],\"scattergeo\":[{\"type\":\"scattergeo\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolar\":[{\"type\":\"scatterpolar\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"histogram\":[{\"marker\":{\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"histogram\"}],\"scattergl\":[{\"type\":\"scattergl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatter3d\":[{\"type\":\"scatter3d\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattermapbox\":[{\"type\":\"scattermapbox\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterternary\":[{\"type\":\"scatterternary\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattercarpet\":[{\"type\":\"scattercarpet\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"carpet\":[{\"aaxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"baxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"type\":\"carpet\"}],\"table\":[{\"cells\":{\"fill\":{\"color\":\"#EBF0F8\"},\"line\":{\"color\":\"white\"}},\"header\":{\"fill\":{\"color\":\"#C8D4E3\"},\"line\":{\"color\":\"white\"}},\"type\":\"table\"}],\"barpolar\":[{\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"barpolar\"}],\"pie\":[{\"automargin\":true,\"type\":\"pie\"}]},\"layout\":{\"autotypenumbers\":\"strict\",\"colorway\":[\"#636efa\",\"#EF553B\",\"#00cc96\",\"#ab63fa\",\"#FFA15A\",\"#19d3f3\",\"#FF6692\",\"#B6E880\",\"#FF97FF\",\"#FECB52\"],\"font\":{\"color\":\"#2a3f5f\"},\"hovermode\":\"closest\",\"hoverlabel\":{\"align\":\"left\"},\"paper_bgcolor\":\"white\",\"plot_bgcolor\":\"#E5ECF6\",\"polar\":{\"bgcolor\":\"#E5ECF6\",\"angularaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"radialaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"ternary\":{\"bgcolor\":\"#E5ECF6\",\"aaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"baxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"caxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"coloraxis\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"colorscale\":{\"sequential\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"sequentialminus\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"diverging\":[[0,\"#8e0152\"],[0.1,\"#c51b7d\"],[0.2,\"#de77ae\"],[0.3,\"#f1b6da\"],[0.4,\"#fde0ef\"],[0.5,\"#f7f7f7\"],[0.6,\"#e6f5d0\"],[0.7,\"#b8e186\"],[0.8,\"#7fbc41\"],[0.9,\"#4d9221\"],[1,\"#276419\"]]},\"xaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"yaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"scene\":{\"xaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"yaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"zaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2}},\"shapedefaults\":{\"line\":{\"color\":\"#2a3f5f\"}},\"annotationdefaults\":{\"arrowcolor\":\"#2a3f5f\",\"arrowhead\":0,\"arrowwidth\":1},\"geo\":{\"bgcolor\":\"white\",\"landcolor\":\"#E5ECF6\",\"subunitcolor\":\"white\",\"showland\":true,\"showlakes\":true,\"lakecolor\":\"white\"},\"title\":{\"x\":0.05},\"mapbox\":{\"style\":\"light\"}}},\"xaxis\":{\"anchor\":\"y\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Number Of Ratings\"}},\"yaxis\":{\"anchor\":\"x\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Sale Price\"}},\"legend\":{\"tracegroupgap\":0,\"itemsizing\":\"constant\"},\"title\":{\"text\":\"Relationship between Sale Price and Number of Ratings of iPhones 8\"}},                        {\"responsive\": true}                    ).then(function(){\n",
              "                            \n",
              "var gd = document.getElementById('d775a701-b656-4935-a115-0f55d701e9d8');\n",
              "var x = new MutationObserver(function (mutations, observer) {{\n",
              "        var display = window.getComputedStyle(gd).display;\n",
              "        if (!display || display === 'none') {{\n",
              "            console.log([gd, 'removed!']);\n",
              "            Plotly.purge(gd);\n",
              "            observer.disconnect();\n",
              "        }}\n",
              "}});\n",
              "\n",
              "// Listen for the removal of the full notebook cells\n",
              "var notebookContainer = gd.closest('#notebook-container');\n",
              "if (notebookContainer) {{\n",
              "    x.observe(notebookContainer, {childList: true});\n",
              "}}\n",
              "\n",
              "// Listen for the clearing of the current output cell\n",
              "var outputEl = gd.closest('.output');\n",
              "if (outputEl) {{\n",
              "    x.observe(outputEl, {childList: true});\n",
              "}}\n",
              "\n",
              "                        })                };                            </script>        </div>\n",
              "</body>\n",
              "</html>"
            ]
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "iphone_xr = df.iloc[9:14]"
      ],
      "metadata": {
        "id": "n6W1eSsfpHRq"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "counts_xr = iphone_xr[\"Number Of Ratings\"]\n",
        "fig = px.bar(iphone_xr, x='Product Name', y = counts_xr,)\n",
        "\n",
        "fig.show()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 542
        },
        "id": "IOReoT4ZpHVA",
        "outputId": "4c1c6c36-3631-434b-992b-945885e8a596"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/html": [
              "<html>\n",
              "<head><meta charset=\"utf-8\" /></head>\n",
              "<body>\n",
              "    <div>            <script src=\"https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG\"></script><script type=\"text/javascript\">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: \"STIX-Web\"}});}</script>                <script type=\"text/javascript\">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>\n",
              "        <script charset=\"utf-8\" src=\"https://cdn.plot.ly/plotly-2.24.1.min.js\"></script>                <div id=\"ad184221-8c23-41e7-bd5a-480e51d49e1d\" class=\"plotly-graph-div\" style=\"height:525px; width:100%;\"></div>            <script type=\"text/javascript\">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById(\"ad184221-8c23-41e7-bd5a-480e51d49e1d\")) {                    Plotly.newPlot(                        \"ad184221-8c23-41e7-bd5a-480e51d49e1d\",                        [{\"alignmentgroup\":\"True\",\"hovertemplate\":\"Product Name=%{x}\\u003cbr\\u003eNumber Of Ratings=%{y}\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"pattern\":{\"shape\":\"\"}},\"name\":\"\",\"offsetgroup\":\"\",\"orientation\":\"v\",\"showlegend\":false,\"textposition\":\"auto\",\"x\":[\"Apple iPhone XR ((PRODUCT)RED, 128 GB) (Includes EarPods, Power Adapter)\",\"Apple iPhone XR (Black, 64 GB) (Includes EarPods, Power Adapter)\",\"Apple iPhone XR (Coral, 128 GB) (Includes EarPods, Power Adapter)\",\"Apple iPhone XR (Black, 128 GB) (Includes EarPods, Power Adapter)\",\"Apple iPhone XR (White, 128 GB) (Includes EarPods, Power Adapter)\"],\"xaxis\":\"x\",\"y\":[79512,79512,79582,79512,79512],\"yaxis\":\"y\",\"type\":\"bar\"}],                        {\"template\":{\"data\":{\"histogram2dcontour\":[{\"type\":\"histogram2dcontour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"choropleth\":[{\"type\":\"choropleth\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"histogram2d\":[{\"type\":\"histogram2d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmap\":[{\"type\":\"heatmap\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmapgl\":[{\"type\":\"heatmapgl\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"contourcarpet\":[{\"type\":\"contourcarpet\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"contour\":[{\"type\":\"contour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"surface\":[{\"type\":\"surface\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"mesh3d\":[{\"type\":\"mesh3d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"scatter\":[{\"fillpattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2},\"type\":\"scatter\"}],\"parcoords\":[{\"type\":\"parcoords\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolargl\":[{\"type\":\"scatterpolargl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"bar\":[{\"error_x\":{\"color\":\"#2a3f5f\"},\"error_y\":{\"color\":\"#2a3f5f\"},\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"bar\"}],\"scattergeo\":[{\"type\":\"scattergeo\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolar\":[{\"type\":\"scatterpolar\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"histogram\":[{\"marker\":{\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"histogram\"}],\"scattergl\":[{\"type\":\"scattergl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatter3d\":[{\"type\":\"scatter3d\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattermapbox\":[{\"type\":\"scattermapbox\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterternary\":[{\"type\":\"scatterternary\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattercarpet\":[{\"type\":\"scattercarpet\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"carpet\":[{\"aaxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"baxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"type\":\"carpet\"}],\"table\":[{\"cells\":{\"fill\":{\"color\":\"#EBF0F8\"},\"line\":{\"color\":\"white\"}},\"header\":{\"fill\":{\"color\":\"#C8D4E3\"},\"line\":{\"color\":\"white\"}},\"type\":\"table\"}],\"barpolar\":[{\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"barpolar\"}],\"pie\":[{\"automargin\":true,\"type\":\"pie\"}]},\"layout\":{\"autotypenumbers\":\"strict\",\"colorway\":[\"#636efa\",\"#EF553B\",\"#00cc96\",\"#ab63fa\",\"#FFA15A\",\"#19d3f3\",\"#FF6692\",\"#B6E880\",\"#FF97FF\",\"#FECB52\"],\"font\":{\"color\":\"#2a3f5f\"},\"hovermode\":\"closest\",\"hoverlabel\":{\"align\":\"left\"},\"paper_bgcolor\":\"white\",\"plot_bgcolor\":\"#E5ECF6\",\"polar\":{\"bgcolor\":\"#E5ECF6\",\"angularaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"radialaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"ternary\":{\"bgcolor\":\"#E5ECF6\",\"aaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"baxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"caxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"coloraxis\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"colorscale\":{\"sequential\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"sequentialminus\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"diverging\":[[0,\"#8e0152\"],[0.1,\"#c51b7d\"],[0.2,\"#de77ae\"],[0.3,\"#f1b6da\"],[0.4,\"#fde0ef\"],[0.5,\"#f7f7f7\"],[0.6,\"#e6f5d0\"],[0.7,\"#b8e186\"],[0.8,\"#7fbc41\"],[0.9,\"#4d9221\"],[1,\"#276419\"]]},\"xaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"yaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"scene\":{\"xaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"yaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"zaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2}},\"shapedefaults\":{\"line\":{\"color\":\"#2a3f5f\"}},\"annotationdefaults\":{\"arrowcolor\":\"#2a3f5f\",\"arrowhead\":0,\"arrowwidth\":1},\"geo\":{\"bgcolor\":\"white\",\"landcolor\":\"#E5ECF6\",\"subunitcolor\":\"white\",\"showland\":true,\"showlakes\":true,\"lakecolor\":\"white\"},\"title\":{\"x\":0.05},\"mapbox\":{\"style\":\"light\"}}},\"xaxis\":{\"anchor\":\"y\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Product Name\"}},\"yaxis\":{\"anchor\":\"x\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Number Of Ratings\"}},\"legend\":{\"tracegroupgap\":0},\"margin\":{\"t\":60},\"barmode\":\"relative\"},                        {\"responsive\": true}                    ).then(function(){\n",
              "                            \n",
              "var gd = document.getElementById('ad184221-8c23-41e7-bd5a-480e51d49e1d');\n",
              "var x = new MutationObserver(function (mutations, observer) {{\n",
              "        var display = window.getComputedStyle(gd).display;\n",
              "        if (!display || display === 'none') {{\n",
              "            console.log([gd, 'removed!']);\n",
              "            Plotly.purge(gd);\n",
              "            observer.disconnect();\n",
              "        }}\n",
              "}});\n",
              "\n",
              "// Listen for the removal of the full notebook cells\n",
              "var notebookContainer = gd.closest('#notebook-container');\n",
              "if (notebookContainer) {{\n",
              "    x.observe(notebookContainer, {childList: true});\n",
              "}}\n",
              "\n",
              "// Listen for the clearing of the current output cell\n",
              "var outputEl = gd.closest('.output');\n",
              "if (outputEl) {{\n",
              "    x.observe(outputEl, {childList: true});\n",
              "}}\n",
              "\n",
              "                        })                };                            </script>        </div>\n",
              "</body>\n",
              "</html>"
            ]
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "Iphone XR Number Of Ratings พอๆกันหมด"
      ],
      "metadata": {
        "id": "IcGoeHa8pwc9"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "figure = px.scatter(data_frame = iphone_xr, x=\"Number Of Ratings\",\n",
        "                    y=\"Sale Price\", size=\"Discount Percentage\",\n",
        "                    trendline=\"ols\",\n",
        "                    title=\"Relationship between Sale Price and Number of Ratings of iPhones xr\")\n",
        "figure.show()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 542
        },
        "id": "HfbC23a0sAyk",
        "outputId": "36f2e95f-2d83-4c9f-da02-f577abe9537b"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/html": [
              "<html>\n",
              "<head><meta charset=\"utf-8\" /></head>\n",
              "<body>\n",
              "    <div>            <script src=\"https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG\"></script><script type=\"text/javascript\">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: \"STIX-Web\"}});}</script>                <script type=\"text/javascript\">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>\n",
              "        <script charset=\"utf-8\" src=\"https://cdn.plot.ly/plotly-2.24.1.min.js\"></script>                <div id=\"916e39c5-5594-449d-8735-b3a78c7bb00c\" class=\"plotly-graph-div\" style=\"height:525px; width:100%;\"></div>            <script type=\"text/javascript\">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById(\"916e39c5-5594-449d-8735-b3a78c7bb00c\")) {                    Plotly.newPlot(                        \"916e39c5-5594-449d-8735-b3a78c7bb00c\",                        [{\"hovertemplate\":\"Number Of Ratings=%{x}\\u003cbr\\u003eSale Price=%{y}\\u003cbr\\u003eDiscount Percentage=%{marker.size}\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"size\":[0,0,0,29,15,0,15,17],\"sizemode\":\"area\",\"sizeref\":0.0725,\"symbol\":\"circle\"},\"mode\":\"markers\",\"name\":\"\",\"orientation\":\"v\",\"showlegend\":false,\"x\":[1078,1078,1078,7088,7088,1078,7088,7081],\"xaxis\":\"x\",\"y\":[117100,131900,117100,74999,117900,117100,117900,99900],\"yaxis\":\"y\",\"type\":\"scatter\"},{\"hovertemplate\":\"\\u003cb\\u003eOLS trendline\\u003c\\u002fb\\u003e\\u003cbr\\u003eSale Price = -3.01646 * Number Of Ratings + 124051\\u003cbr\\u003eR\\u003csup\\u003e2\\u003c\\u002fsup\\u003e=0.319117\\u003cbr\\u003e\\u003cbr\\u003eNumber Of Ratings=%{x}\\u003cbr\\u003eSale Price=%{y} \\u003cb\\u003e(trend)\\u003c\\u002fb\\u003e\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"symbol\":\"circle\"},\"mode\":\"lines\",\"name\":\"\",\"showlegend\":false,\"x\":[1078,1078,1078,1078,7081,7088,7088,7088],\"xaxis\":\"x\",\"y\":[120799.18719657243,120799.18719657243,120799.18719657243,120799.18719657243,102691.39919972664,102670.2840046612,102670.2840046612,102670.2840046612],\"yaxis\":\"y\",\"type\":\"scatter\"}],                        {\"template\":{\"data\":{\"histogram2dcontour\":[{\"type\":\"histogram2dcontour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"choropleth\":[{\"type\":\"choropleth\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"histogram2d\":[{\"type\":\"histogram2d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmap\":[{\"type\":\"heatmap\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmapgl\":[{\"type\":\"heatmapgl\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"contourcarpet\":[{\"type\":\"contourcarpet\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"contour\":[{\"type\":\"contour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"surface\":[{\"type\":\"surface\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"mesh3d\":[{\"type\":\"mesh3d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"scatter\":[{\"fillpattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2},\"type\":\"scatter\"}],\"parcoords\":[{\"type\":\"parcoords\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolargl\":[{\"type\":\"scatterpolargl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"bar\":[{\"error_x\":{\"color\":\"#2a3f5f\"},\"error_y\":{\"color\":\"#2a3f5f\"},\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"bar\"}],\"scattergeo\":[{\"type\":\"scattergeo\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolar\":[{\"type\":\"scatterpolar\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"histogram\":[{\"marker\":{\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"histogram\"}],\"scattergl\":[{\"type\":\"scattergl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatter3d\":[{\"type\":\"scatter3d\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattermapbox\":[{\"type\":\"scattermapbox\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterternary\":[{\"type\":\"scatterternary\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattercarpet\":[{\"type\":\"scattercarpet\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"carpet\":[{\"aaxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"baxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"type\":\"carpet\"}],\"table\":[{\"cells\":{\"fill\":{\"color\":\"#EBF0F8\"},\"line\":{\"color\":\"white\"}},\"header\":{\"fill\":{\"color\":\"#C8D4E3\"},\"line\":{\"color\":\"white\"}},\"type\":\"table\"}],\"barpolar\":[{\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"barpolar\"}],\"pie\":[{\"automargin\":true,\"type\":\"pie\"}]},\"layout\":{\"autotypenumbers\":\"strict\",\"colorway\":[\"#636efa\",\"#EF553B\",\"#00cc96\",\"#ab63fa\",\"#FFA15A\",\"#19d3f3\",\"#FF6692\",\"#B6E880\",\"#FF97FF\",\"#FECB52\"],\"font\":{\"color\":\"#2a3f5f\"},\"hovermode\":\"closest\",\"hoverlabel\":{\"align\":\"left\"},\"paper_bgcolor\":\"white\",\"plot_bgcolor\":\"#E5ECF6\",\"polar\":{\"bgcolor\":\"#E5ECF6\",\"angularaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"radialaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"ternary\":{\"bgcolor\":\"#E5ECF6\",\"aaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"baxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"caxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"coloraxis\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"colorscale\":{\"sequential\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"sequentialminus\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"diverging\":[[0,\"#8e0152\"],[0.1,\"#c51b7d\"],[0.2,\"#de77ae\"],[0.3,\"#f1b6da\"],[0.4,\"#fde0ef\"],[0.5,\"#f7f7f7\"],[0.6,\"#e6f5d0\"],[0.7,\"#b8e186\"],[0.8,\"#7fbc41\"],[0.9,\"#4d9221\"],[1,\"#276419\"]]},\"xaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"yaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"scene\":{\"xaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"yaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"zaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2}},\"shapedefaults\":{\"line\":{\"color\":\"#2a3f5f\"}},\"annotationdefaults\":{\"arrowcolor\":\"#2a3f5f\",\"arrowhead\":0,\"arrowwidth\":1},\"geo\":{\"bgcolor\":\"white\",\"landcolor\":\"#E5ECF6\",\"subunitcolor\":\"white\",\"showland\":true,\"showlakes\":true,\"lakecolor\":\"white\"},\"title\":{\"x\":0.05},\"mapbox\":{\"style\":\"light\"}}},\"xaxis\":{\"anchor\":\"y\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Number Of Ratings\"}},\"yaxis\":{\"anchor\":\"x\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Sale Price\"}},\"legend\":{\"tracegroupgap\":0,\"itemsizing\":\"constant\"},\"title\":{\"text\":\"Relationship between Sale Price and Number of Ratings of iPhones xr\"}},                        {\"responsive\": true}                    ).then(function(){\n",
              "                            \n",
              "var gd = document.getElementById('916e39c5-5594-449d-8735-b3a78c7bb00c');\n",
              "var x = new MutationObserver(function (mutations, observer) {{\n",
              "        var display = window.getComputedStyle(gd).display;\n",
              "        if (!display || display === 'none') {{\n",
              "            console.log([gd, 'removed!']);\n",
              "            Plotly.purge(gd);\n",
              "            observer.disconnect();\n",
              "        }}\n",
              "}});\n",
              "\n",
              "// Listen for the removal of the full notebook cells\n",
              "var notebookContainer = gd.closest('#notebook-container');\n",
              "if (notebookContainer) {{\n",
              "    x.observe(notebookContainer, {childList: true});\n",
              "}}\n",
              "\n",
              "// Listen for the clearing of the current output cell\n",
              "var outputEl = gd.closest('.output');\n",
              "if (outputEl) {{\n",
              "    x.observe(outputEl, {childList: true});\n",
              "}}\n",
              "\n",
              "                        })                };                            </script>        </div>\n",
              "</body>\n",
              "</html>"
            ]
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "iphone_11 = df.iloc[15:23]"
      ],
      "metadata": {
        "id": "Jul4azEupHZf"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "counts_11 = iphone_11[\"Number Of Ratings\"]\n",
        "fig = px.bar(iphone_11, x='Product Name', y = counts_11,)\n",
        "\n",
        "fig.show()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 542
        },
        "id": "DK87yqMmqZSh",
        "outputId": "52e0d896-b097-4dbd-e530-93463c10223f"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/html": [
              "<html>\n",
              "<head><meta charset=\"utf-8\" /></head>\n",
              "<body>\n",
              "    <div>            <script src=\"https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG\"></script><script type=\"text/javascript\">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: \"STIX-Web\"}});}</script>                <script type=\"text/javascript\">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>\n",
              "        <script charset=\"utf-8\" src=\"https://cdn.plot.ly/plotly-2.24.1.min.js\"></script>                <div id=\"f578d713-71e3-4d59-85a9-ec6087c4c59a\" class=\"plotly-graph-div\" style=\"height:525px; width:100%;\"></div>            <script type=\"text/javascript\">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById(\"f578d713-71e3-4d59-85a9-ec6087c4c59a\")) {                    Plotly.newPlot(                        \"f578d713-71e3-4d59-85a9-ec6087c4c59a\",                        [{\"alignmentgroup\":\"True\",\"hovertemplate\":\"Product Name=%{x}\\u003cbr\\u003eNumber Of Ratings=%{y}\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"pattern\":{\"shape\":\"\"}},\"name\":\"\",\"offsetgroup\":\"\",\"orientation\":\"v\",\"showlegend\":false,\"textposition\":\"auto\",\"x\":[\"APPLE iPhone 11 Pro Max (Gold, 64 GB)\",\"APPLE iPhone 11 Pro Max (Midnight Green, 256 GB)\",\"APPLE iPhone 11 Pro Max (Space Grey, 64 GB)\",\"APPLE iPhone 11 Pro (Midnight Green, 64 GB)\",\"APPLE iPhone 11 Pro (Space Grey, 512 GB)\",\"APPLE iPhone 11 Pro Max (Midnight Green, 64 GB)\",\"APPLE iPhone 11 Pro (Midnight Green, 512 GB)\",\"APPLE iPhone 11 Pro (Space Grey, 256 GB)\"],\"xaxis\":\"x\",\"y\":[1078,1078,1078,7088,7088,1078,7088,7081],\"yaxis\":\"y\",\"type\":\"bar\"}],                        {\"template\":{\"data\":{\"histogram2dcontour\":[{\"type\":\"histogram2dcontour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"choropleth\":[{\"type\":\"choropleth\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"histogram2d\":[{\"type\":\"histogram2d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmap\":[{\"type\":\"heatmap\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmapgl\":[{\"type\":\"heatmapgl\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"contourcarpet\":[{\"type\":\"contourcarpet\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"contour\":[{\"type\":\"contour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"surface\":[{\"type\":\"surface\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"mesh3d\":[{\"type\":\"mesh3d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"scatter\":[{\"fillpattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2},\"type\":\"scatter\"}],\"parcoords\":[{\"type\":\"parcoords\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolargl\":[{\"type\":\"scatterpolargl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"bar\":[{\"error_x\":{\"color\":\"#2a3f5f\"},\"error_y\":{\"color\":\"#2a3f5f\"},\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"bar\"}],\"scattergeo\":[{\"type\":\"scattergeo\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolar\":[{\"type\":\"scatterpolar\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"histogram\":[{\"marker\":{\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"histogram\"}],\"scattergl\":[{\"type\":\"scattergl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatter3d\":[{\"type\":\"scatter3d\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattermapbox\":[{\"type\":\"scattermapbox\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterternary\":[{\"type\":\"scatterternary\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattercarpet\":[{\"type\":\"scattercarpet\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"carpet\":[{\"aaxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"baxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"type\":\"carpet\"}],\"table\":[{\"cells\":{\"fill\":{\"color\":\"#EBF0F8\"},\"line\":{\"color\":\"white\"}},\"header\":{\"fill\":{\"color\":\"#C8D4E3\"},\"line\":{\"color\":\"white\"}},\"type\":\"table\"}],\"barpolar\":[{\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"barpolar\"}],\"pie\":[{\"automargin\":true,\"type\":\"pie\"}]},\"layout\":{\"autotypenumbers\":\"strict\",\"colorway\":[\"#636efa\",\"#EF553B\",\"#00cc96\",\"#ab63fa\",\"#FFA15A\",\"#19d3f3\",\"#FF6692\",\"#B6E880\",\"#FF97FF\",\"#FECB52\"],\"font\":{\"color\":\"#2a3f5f\"},\"hovermode\":\"closest\",\"hoverlabel\":{\"align\":\"left\"},\"paper_bgcolor\":\"white\",\"plot_bgcolor\":\"#E5ECF6\",\"polar\":{\"bgcolor\":\"#E5ECF6\",\"angularaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"radialaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"ternary\":{\"bgcolor\":\"#E5ECF6\",\"aaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"baxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"caxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"coloraxis\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"colorscale\":{\"sequential\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"sequentialminus\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"diverging\":[[0,\"#8e0152\"],[0.1,\"#c51b7d\"],[0.2,\"#de77ae\"],[0.3,\"#f1b6da\"],[0.4,\"#fde0ef\"],[0.5,\"#f7f7f7\"],[0.6,\"#e6f5d0\"],[0.7,\"#b8e186\"],[0.8,\"#7fbc41\"],[0.9,\"#4d9221\"],[1,\"#276419\"]]},\"xaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"yaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"scene\":{\"xaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"yaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"zaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2}},\"shapedefaults\":{\"line\":{\"color\":\"#2a3f5f\"}},\"annotationdefaults\":{\"arrowcolor\":\"#2a3f5f\",\"arrowhead\":0,\"arrowwidth\":1},\"geo\":{\"bgcolor\":\"white\",\"landcolor\":\"#E5ECF6\",\"subunitcolor\":\"white\",\"showland\":true,\"showlakes\":true,\"lakecolor\":\"white\"},\"title\":{\"x\":0.05},\"mapbox\":{\"style\":\"light\"}}},\"xaxis\":{\"anchor\":\"y\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Product Name\"}},\"yaxis\":{\"anchor\":\"x\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Number Of Ratings\"}},\"legend\":{\"tracegroupgap\":0},\"margin\":{\"t\":60},\"barmode\":\"relative\"},                        {\"responsive\": true}                    ).then(function(){\n",
              "                            \n",
              "var gd = document.getElementById('f578d713-71e3-4d59-85a9-ec6087c4c59a');\n",
              "var x = new MutationObserver(function (mutations, observer) {{\n",
              "        var display = window.getComputedStyle(gd).display;\n",
              "        if (!display || display === 'none') {{\n",
              "            console.log([gd, 'removed!']);\n",
              "            Plotly.purge(gd);\n",
              "            observer.disconnect();\n",
              "        }}\n",
              "}});\n",
              "\n",
              "// Listen for the removal of the full notebook cells\n",
              "var notebookContainer = gd.closest('#notebook-container');\n",
              "if (notebookContainer) {{\n",
              "    x.observe(notebookContainer, {childList: true});\n",
              "}}\n",
              "\n",
              "// Listen for the clearing of the current output cell\n",
              "var outputEl = gd.closest('.output');\n",
              "if (outputEl) {{\n",
              "    x.observe(outputEl, {childList: true});\n",
              "}}\n",
              "\n",
              "                        })                };                            </script>        </div>\n",
              "</body>\n",
              "</html>"
            ]
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "figure = px.scatter(data_frame = iphone_11, x=\"Number Of Ratings\",\n",
        "                    y=\"Sale Price\", size=\"Discount Percentage\",\n",
        "                    trendline=\"ols\",\n",
        "                    title=\"Relationship between Sale Price and Number of Ratings of iPhones 11\")\n",
        "figure.show()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 542
        },
        "id": "kT2lI2yVsLEj",
        "outputId": "326ca6a7-78c4-4f03-d008-234de8902d5f"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/html": [
              "<html>\n",
              "<head><meta charset=\"utf-8\" /></head>\n",
              "<body>\n",
              "    <div>            <script src=\"https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG\"></script><script type=\"text/javascript\">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: \"STIX-Web\"}});}</script>                <script type=\"text/javascript\">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>\n",
              "        <script charset=\"utf-8\" src=\"https://cdn.plot.ly/plotly-2.24.1.min.js\"></script>                <div id=\"20e2e4d7-2f69-49cc-a9b8-5d0aa98dba06\" class=\"plotly-graph-div\" style=\"height:525px; width:100%;\"></div>            <script type=\"text/javascript\">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById(\"20e2e4d7-2f69-49cc-a9b8-5d0aa98dba06\")) {                    Plotly.newPlot(                        \"20e2e4d7-2f69-49cc-a9b8-5d0aa98dba06\",                        [{\"hovertemplate\":\"Number Of Ratings=%{x}\\u003cbr\\u003eSale Price=%{y}\\u003cbr\\u003eDiscount Percentage=%{marker.size}\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"size\":[0,0,0,29,15,0,15,17],\"sizemode\":\"area\",\"sizeref\":0.0725,\"symbol\":\"circle\"},\"mode\":\"markers\",\"name\":\"\",\"orientation\":\"v\",\"showlegend\":false,\"x\":[1078,1078,1078,7088,7088,1078,7088,7081],\"xaxis\":\"x\",\"y\":[117100,131900,117100,74999,117900,117100,117900,99900],\"yaxis\":\"y\",\"type\":\"scatter\"},{\"hovertemplate\":\"\\u003cb\\u003eOLS trendline\\u003c\\u002fb\\u003e\\u003cbr\\u003eSale Price = -3.01646 * Number Of Ratings + 124051\\u003cbr\\u003eR\\u003csup\\u003e2\\u003c\\u002fsup\\u003e=0.319117\\u003cbr\\u003e\\u003cbr\\u003eNumber Of Ratings=%{x}\\u003cbr\\u003eSale Price=%{y} \\u003cb\\u003e(trend)\\u003c\\u002fb\\u003e\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"symbol\":\"circle\"},\"mode\":\"lines\",\"name\":\"\",\"showlegend\":false,\"x\":[1078,1078,1078,1078,7081,7088,7088,7088],\"xaxis\":\"x\",\"y\":[120799.18719657243,120799.18719657243,120799.18719657243,120799.18719657243,102691.39919972664,102670.2840046612,102670.2840046612,102670.2840046612],\"yaxis\":\"y\",\"type\":\"scatter\"}],                        {\"template\":{\"data\":{\"histogram2dcontour\":[{\"type\":\"histogram2dcontour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"choropleth\":[{\"type\":\"choropleth\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"histogram2d\":[{\"type\":\"histogram2d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmap\":[{\"type\":\"heatmap\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmapgl\":[{\"type\":\"heatmapgl\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"contourcarpet\":[{\"type\":\"contourcarpet\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"contour\":[{\"type\":\"contour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"surface\":[{\"type\":\"surface\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"mesh3d\":[{\"type\":\"mesh3d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"scatter\":[{\"fillpattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2},\"type\":\"scatter\"}],\"parcoords\":[{\"type\":\"parcoords\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolargl\":[{\"type\":\"scatterpolargl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"bar\":[{\"error_x\":{\"color\":\"#2a3f5f\"},\"error_y\":{\"color\":\"#2a3f5f\"},\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"bar\"}],\"scattergeo\":[{\"type\":\"scattergeo\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolar\":[{\"type\":\"scatterpolar\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"histogram\":[{\"marker\":{\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"histogram\"}],\"scattergl\":[{\"type\":\"scattergl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatter3d\":[{\"type\":\"scatter3d\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattermapbox\":[{\"type\":\"scattermapbox\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterternary\":[{\"type\":\"scatterternary\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattercarpet\":[{\"type\":\"scattercarpet\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"carpet\":[{\"aaxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"baxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"type\":\"carpet\"}],\"table\":[{\"cells\":{\"fill\":{\"color\":\"#EBF0F8\"},\"line\":{\"color\":\"white\"}},\"header\":{\"fill\":{\"color\":\"#C8D4E3\"},\"line\":{\"color\":\"white\"}},\"type\":\"table\"}],\"barpolar\":[{\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"barpolar\"}],\"pie\":[{\"automargin\":true,\"type\":\"pie\"}]},\"layout\":{\"autotypenumbers\":\"strict\",\"colorway\":[\"#636efa\",\"#EF553B\",\"#00cc96\",\"#ab63fa\",\"#FFA15A\",\"#19d3f3\",\"#FF6692\",\"#B6E880\",\"#FF97FF\",\"#FECB52\"],\"font\":{\"color\":\"#2a3f5f\"},\"hovermode\":\"closest\",\"hoverlabel\":{\"align\":\"left\"},\"paper_bgcolor\":\"white\",\"plot_bgcolor\":\"#E5ECF6\",\"polar\":{\"bgcolor\":\"#E5ECF6\",\"angularaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"radialaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"ternary\":{\"bgcolor\":\"#E5ECF6\",\"aaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"baxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"caxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"coloraxis\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"colorscale\":{\"sequential\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"sequentialminus\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"diverging\":[[0,\"#8e0152\"],[0.1,\"#c51b7d\"],[0.2,\"#de77ae\"],[0.3,\"#f1b6da\"],[0.4,\"#fde0ef\"],[0.5,\"#f7f7f7\"],[0.6,\"#e6f5d0\"],[0.7,\"#b8e186\"],[0.8,\"#7fbc41\"],[0.9,\"#4d9221\"],[1,\"#276419\"]]},\"xaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"yaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"scene\":{\"xaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"yaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"zaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2}},\"shapedefaults\":{\"line\":{\"color\":\"#2a3f5f\"}},\"annotationdefaults\":{\"arrowcolor\":\"#2a3f5f\",\"arrowhead\":0,\"arrowwidth\":1},\"geo\":{\"bgcolor\":\"white\",\"landcolor\":\"#E5ECF6\",\"subunitcolor\":\"white\",\"showland\":true,\"showlakes\":true,\"lakecolor\":\"white\"},\"title\":{\"x\":0.05},\"mapbox\":{\"style\":\"light\"}}},\"xaxis\":{\"anchor\":\"y\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Number Of Ratings\"}},\"yaxis\":{\"anchor\":\"x\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Sale Price\"}},\"legend\":{\"tracegroupgap\":0,\"itemsizing\":\"constant\"},\"title\":{\"text\":\"Relationship between Sale Price and Number of Ratings of iPhones 11\"}},                        {\"responsive\": true}                    ).then(function(){\n",
              "                            \n",
              "var gd = document.getElementById('20e2e4d7-2f69-49cc-a9b8-5d0aa98dba06');\n",
              "var x = new MutationObserver(function (mutations, observer) {{\n",
              "        var display = window.getComputedStyle(gd).display;\n",
              "        if (!display || display === 'none') {{\n",
              "            console.log([gd, 'removed!']);\n",
              "            Plotly.purge(gd);\n",
              "            observer.disconnect();\n",
              "        }}\n",
              "}});\n",
              "\n",
              "// Listen for the removal of the full notebook cells\n",
              "var notebookContainer = gd.closest('#notebook-container');\n",
              "if (notebookContainer) {{\n",
              "    x.observe(notebookContainer, {childList: true});\n",
              "}}\n",
              "\n",
              "// Listen for the clearing of the current output cell\n",
              "var outputEl = gd.closest('.output');\n",
              "if (outputEl) {{\n",
              "    x.observe(outputEl, {childList: true});\n",
              "}}\n",
              "\n",
              "                        })                };                            </script>        </div>\n",
              "</body>\n",
              "</html>"
            ]
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "ข้อมูลมันแปลกๆจัง5555\n"
      ],
      "metadata": {
        "id": "_0YHgohDqtjS"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "iphone_12 = df.iloc[24:49]"
      ],
      "metadata": {
        "id": "c8kW-qIZrFGY"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "counts_12 = iphone_12[\"Number Of Ratings\"]\n",
        "fig = px.bar(iphone_12, x='Product Name', y = counts_12,)\n",
        "\n",
        "fig.show()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 542
        },
        "id": "aJwgtipPrKgF",
        "outputId": "509492eb-5918-4aa9-c43e-405f31092b2f"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/html": [
              "<html>\n",
              "<head><meta charset=\"utf-8\" /></head>\n",
              "<body>\n",
              "    <div>            <script src=\"https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG\"></script><script type=\"text/javascript\">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: \"STIX-Web\"}});}</script>                <script type=\"text/javascript\">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>\n",
              "        <script charset=\"utf-8\" src=\"https://cdn.plot.ly/plotly-2.24.1.min.js\"></script>                <div id=\"7a981515-0200-4b3b-b132-a82ec7cdba9d\" class=\"plotly-graph-div\" style=\"height:525px; width:100%;\"></div>            <script type=\"text/javascript\">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById(\"7a981515-0200-4b3b-b132-a82ec7cdba9d\")) {                    Plotly.newPlot(                        \"7a981515-0200-4b3b-b132-a82ec7cdba9d\",                        [{\"alignmentgroup\":\"True\",\"hovertemplate\":\"Product Name=%{x}\\u003cbr\\u003eNumber Of Ratings=%{y}\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"pattern\":{\"shape\":\"\"}},\"name\":\"\",\"offsetgroup\":\"\",\"orientation\":\"v\",\"showlegend\":false,\"textposition\":\"auto\",\"x\":[\"APPLE iPhone 12 Pro (Silver, 512 GB)\",\"APPLE iPhone 12 Pro Max (Pacific Blue, 256 GB)\",\"APPLE iPhone 12 Mini (White, 128 GB)\",\"APPLE iPhone 12 Pro (Graphite, 256 GB)\",\"APPLE iPhone 12 Mini (White, 64 GB)\",\"APPLE iPhone 12 (White, 128 GB)\",\"APPLE iPhone 12 Pro (Graphite, 128 GB)\",\"APPLE iPhone 12 Pro Max (Graphite, 256 GB)\",\"APPLE iPhone 12 Pro Max (Graphite, 128 GB)\",\"APPLE iPhone 12 Mini (Black, 128 GB)\",\"APPLE iPhone 12 Mini (Blue, 128 GB)\",\"APPLE iPhone 12 (Black, 128 GB)\",\"APPLE iPhone 12 (Blue, 128 GB)\",\"APPLE iPhone 12 Pro Max (Silver, 128 GB)\",\"APPLE iPhone 12 Mini (Red, 64 GB)\",\"APPLE iPhone 12 Pro Max (Gold, 128 GB)\",\"APPLE iPhone 12 (Green, 128 GB)\",\"APPLE iPhone 12 Pro (Pacific Blue, 512 GB)\",\"APPLE iPhone 12 (White, 64 GB)\",\"APPLE iPhone 12 (Black, 64 GB)\",\"APPLE iPhone 12 (Red, 128 GB)\",\"APPLE iPhone 12 Mini (Black, 64 GB)\",\"APPLE iPhone 12 Pro (Pacific Blue, 128 GB)\",\"APPLE iPhone 12 Pro Max (Pacific Blue, 128 GB)\",\"APPLE iPhone 12 Pro Max (Silver, 256 GB)\"],\"xaxis\":\"x\",\"y\":[542,580,740,545,740,2101,545,580,580,730,730,2101,2101,580,740,580,2092,545,2101,2092,2101,740,545,580,580],\"yaxis\":\"y\",\"type\":\"bar\"}],                        {\"template\":{\"data\":{\"histogram2dcontour\":[{\"type\":\"histogram2dcontour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"choropleth\":[{\"type\":\"choropleth\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"histogram2d\":[{\"type\":\"histogram2d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmap\":[{\"type\":\"heatmap\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmapgl\":[{\"type\":\"heatmapgl\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"contourcarpet\":[{\"type\":\"contourcarpet\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"contour\":[{\"type\":\"contour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"surface\":[{\"type\":\"surface\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"mesh3d\":[{\"type\":\"mesh3d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"scatter\":[{\"fillpattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2},\"type\":\"scatter\"}],\"parcoords\":[{\"type\":\"parcoords\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolargl\":[{\"type\":\"scatterpolargl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"bar\":[{\"error_x\":{\"color\":\"#2a3f5f\"},\"error_y\":{\"color\":\"#2a3f5f\"},\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"bar\"}],\"scattergeo\":[{\"type\":\"scattergeo\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolar\":[{\"type\":\"scatterpolar\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"histogram\":[{\"marker\":{\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"histogram\"}],\"scattergl\":[{\"type\":\"scattergl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatter3d\":[{\"type\":\"scatter3d\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattermapbox\":[{\"type\":\"scattermapbox\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterternary\":[{\"type\":\"scatterternary\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattercarpet\":[{\"type\":\"scattercarpet\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"carpet\":[{\"aaxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"baxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"type\":\"carpet\"}],\"table\":[{\"cells\":{\"fill\":{\"color\":\"#EBF0F8\"},\"line\":{\"color\":\"white\"}},\"header\":{\"fill\":{\"color\":\"#C8D4E3\"},\"line\":{\"color\":\"white\"}},\"type\":\"table\"}],\"barpolar\":[{\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"barpolar\"}],\"pie\":[{\"automargin\":true,\"type\":\"pie\"}]},\"layout\":{\"autotypenumbers\":\"strict\",\"colorway\":[\"#636efa\",\"#EF553B\",\"#00cc96\",\"#ab63fa\",\"#FFA15A\",\"#19d3f3\",\"#FF6692\",\"#B6E880\",\"#FF97FF\",\"#FECB52\"],\"font\":{\"color\":\"#2a3f5f\"},\"hovermode\":\"closest\",\"hoverlabel\":{\"align\":\"left\"},\"paper_bgcolor\":\"white\",\"plot_bgcolor\":\"#E5ECF6\",\"polar\":{\"bgcolor\":\"#E5ECF6\",\"angularaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"radialaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"ternary\":{\"bgcolor\":\"#E5ECF6\",\"aaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"baxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"caxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"coloraxis\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"colorscale\":{\"sequential\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"sequentialminus\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"diverging\":[[0,\"#8e0152\"],[0.1,\"#c51b7d\"],[0.2,\"#de77ae\"],[0.3,\"#f1b6da\"],[0.4,\"#fde0ef\"],[0.5,\"#f7f7f7\"],[0.6,\"#e6f5d0\"],[0.7,\"#b8e186\"],[0.8,\"#7fbc41\"],[0.9,\"#4d9221\"],[1,\"#276419\"]]},\"xaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"yaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"scene\":{\"xaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"yaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"zaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2}},\"shapedefaults\":{\"line\":{\"color\":\"#2a3f5f\"}},\"annotationdefaults\":{\"arrowcolor\":\"#2a3f5f\",\"arrowhead\":0,\"arrowwidth\":1},\"geo\":{\"bgcolor\":\"white\",\"landcolor\":\"#E5ECF6\",\"subunitcolor\":\"white\",\"showland\":true,\"showlakes\":true,\"lakecolor\":\"white\"},\"title\":{\"x\":0.05},\"mapbox\":{\"style\":\"light\"}}},\"xaxis\":{\"anchor\":\"y\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Product Name\"}},\"yaxis\":{\"anchor\":\"x\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Number Of Ratings\"}},\"legend\":{\"tracegroupgap\":0},\"margin\":{\"t\":60},\"barmode\":\"relative\"},                        {\"responsive\": true}                    ).then(function(){\n",
              "                            \n",
              "var gd = document.getElementById('7a981515-0200-4b3b-b132-a82ec7cdba9d');\n",
              "var x = new MutationObserver(function (mutations, observer) {{\n",
              "        var display = window.getComputedStyle(gd).display;\n",
              "        if (!display || display === 'none') {{\n",
              "            console.log([gd, 'removed!']);\n",
              "            Plotly.purge(gd);\n",
              "            observer.disconnect();\n",
              "        }}\n",
              "}});\n",
              "\n",
              "// Listen for the removal of the full notebook cells\n",
              "var notebookContainer = gd.closest('#notebook-container');\n",
              "if (notebookContainer) {{\n",
              "    x.observe(notebookContainer, {childList: true});\n",
              "}}\n",
              "\n",
              "// Listen for the clearing of the current output cell\n",
              "var outputEl = gd.closest('.output');\n",
              "if (outputEl) {{\n",
              "    x.observe(outputEl, {childList: true});\n",
              "}}\n",
              "\n",
              "                        })                };                            </script>        </div>\n",
              "</body>\n",
              "</html>"
            ]
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "figure = px.scatter(data_frame = iphone_12, x=\"Number Of Ratings\",\n",
        "                    y=\"Sale Price\", size=\"Discount Percentage\",\n",
        "                    trendline=\"ols\",\n",
        "                    title=\"Relationship between Sale Price and Number of Ratings of iPhones 12\")\n",
        "figure.show()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 542
        },
        "id": "CbLUQCeksVqO",
        "outputId": "1d83e4a6-bfb5-47da-87ad-455cb2772724"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/html": [
              "<html>\n",
              "<head><meta charset=\"utf-8\" /></head>\n",
              "<body>\n",
              "    <div>            <script src=\"https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG\"></script><script type=\"text/javascript\">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: \"STIX-Web\"}});}</script>                <script type=\"text/javascript\">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>\n",
              "        <script charset=\"utf-8\" src=\"https://cdn.plot.ly/plotly-2.24.1.min.js\"></script>                <div id=\"09c84a70-a89b-44f2-9d8a-3884588cca4d\" class=\"plotly-graph-div\" style=\"height:525px; width:100%;\"></div>            <script type=\"text/javascript\">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById(\"09c84a70-a89b-44f2-9d8a-3884588cca4d\")) {                    Plotly.newPlot(                        \"09c84a70-a89b-44f2-9d8a-3884588cca4d\",                        [{\"hovertemplate\":\"Number Of Ratings=%{x}\\u003cbr\\u003eSale Price=%{y}\\u003cbr\\u003eDiscount Percentage=%{marker.size}\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"size\":[6,6,13,6,14,10,7,6,6,13,13,10,10,6,14,6,10,6,11,11,10,14,7,6,6],\"sizemode\":\"area\",\"sizeref\":0.035,\"symbol\":\"circle\"},\"mode\":\"markers\",\"name\":\"\",\"orientation\":\"v\",\"showlegend\":false,\"x\":[542,580,740,545,740,2101,545,580,580,730,730,2101,2101,580,740,580,2092,545,2101,2092,2101,740,545,580,580],\"xaxis\":\"x\",\"y\":[140900,130900,64900,120900,59900,75900,110900,130900,120900,64900,64900,75900,75900,120900,59900,120900,75900,140900,70900,70900,75900,59900,110900,120900,130900],\"yaxis\":\"y\",\"type\":\"scatter\"},{\"hovertemplate\":\"\\u003cb\\u003eOLS trendline\\u003c\\u002fb\\u003e\\u003cbr\\u003eSale Price = -23.7808 * Number Of Ratings + 120488\\u003cbr\\u003eR\\u003csup\\u003e2\\u003c\\u002fsup\\u003e=0.294502\\u003cbr\\u003e\\u003cbr\\u003eNumber Of Ratings=%{x}\\u003cbr\\u003eSale Price=%{y} \\u003cb\\u003e(trend)\\u003c\\u002fb\\u003e\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"symbol\":\"circle\"},\"mode\":\"lines\",\"name\":\"\",\"showlegend\":false,\"x\":[542,545,545,545,545,580,580,580,580,580,580,580,730,730,740,740,740,740,2092,2092,2101,2101,2101,2101,2101],\"xaxis\":\"x\",\"y\":[107599.16053706709,107527.81809802001,107527.81809802001,107527.81809802001,107527.81809802001,106695.48964247073,106695.48964247073,106695.48964247073,106695.48964247073,106695.48964247073,106695.48964247073,106695.48964247073,103128.36769011665,103128.36769011665,102890.55955995971,102890.55955995971,102890.55955995971,102890.55955995971,70738.90036274164,70738.90036274164,70524.8730456004,70524.8730456004,70524.8730456004,70524.8730456004,70524.8730456004],\"yaxis\":\"y\",\"type\":\"scatter\"}],                        {\"template\":{\"data\":{\"histogram2dcontour\":[{\"type\":\"histogram2dcontour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"choropleth\":[{\"type\":\"choropleth\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"histogram2d\":[{\"type\":\"histogram2d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmap\":[{\"type\":\"heatmap\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmapgl\":[{\"type\":\"heatmapgl\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"contourcarpet\":[{\"type\":\"contourcarpet\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"contour\":[{\"type\":\"contour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"surface\":[{\"type\":\"surface\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"mesh3d\":[{\"type\":\"mesh3d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"scatter\":[{\"fillpattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2},\"type\":\"scatter\"}],\"parcoords\":[{\"type\":\"parcoords\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolargl\":[{\"type\":\"scatterpolargl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"bar\":[{\"error_x\":{\"color\":\"#2a3f5f\"},\"error_y\":{\"color\":\"#2a3f5f\"},\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"bar\"}],\"scattergeo\":[{\"type\":\"scattergeo\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolar\":[{\"type\":\"scatterpolar\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"histogram\":[{\"marker\":{\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"histogram\"}],\"scattergl\":[{\"type\":\"scattergl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatter3d\":[{\"type\":\"scatter3d\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattermapbox\":[{\"type\":\"scattermapbox\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterternary\":[{\"type\":\"scatterternary\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattercarpet\":[{\"type\":\"scattercarpet\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"carpet\":[{\"aaxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"baxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"type\":\"carpet\"}],\"table\":[{\"cells\":{\"fill\":{\"color\":\"#EBF0F8\"},\"line\":{\"color\":\"white\"}},\"header\":{\"fill\":{\"color\":\"#C8D4E3\"},\"line\":{\"color\":\"white\"}},\"type\":\"table\"}],\"barpolar\":[{\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"barpolar\"}],\"pie\":[{\"automargin\":true,\"type\":\"pie\"}]},\"layout\":{\"autotypenumbers\":\"strict\",\"colorway\":[\"#636efa\",\"#EF553B\",\"#00cc96\",\"#ab63fa\",\"#FFA15A\",\"#19d3f3\",\"#FF6692\",\"#B6E880\",\"#FF97FF\",\"#FECB52\"],\"font\":{\"color\":\"#2a3f5f\"},\"hovermode\":\"closest\",\"hoverlabel\":{\"align\":\"left\"},\"paper_bgcolor\":\"white\",\"plot_bgcolor\":\"#E5ECF6\",\"polar\":{\"bgcolor\":\"#E5ECF6\",\"angularaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"radialaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"ternary\":{\"bgcolor\":\"#E5ECF6\",\"aaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"baxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"caxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"coloraxis\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"colorscale\":{\"sequential\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"sequentialminus\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"diverging\":[[0,\"#8e0152\"],[0.1,\"#c51b7d\"],[0.2,\"#de77ae\"],[0.3,\"#f1b6da\"],[0.4,\"#fde0ef\"],[0.5,\"#f7f7f7\"],[0.6,\"#e6f5d0\"],[0.7,\"#b8e186\"],[0.8,\"#7fbc41\"],[0.9,\"#4d9221\"],[1,\"#276419\"]]},\"xaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"yaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"scene\":{\"xaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"yaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"zaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2}},\"shapedefaults\":{\"line\":{\"color\":\"#2a3f5f\"}},\"annotationdefaults\":{\"arrowcolor\":\"#2a3f5f\",\"arrowhead\":0,\"arrowwidth\":1},\"geo\":{\"bgcolor\":\"white\",\"landcolor\":\"#E5ECF6\",\"subunitcolor\":\"white\",\"showland\":true,\"showlakes\":true,\"lakecolor\":\"white\"},\"title\":{\"x\":0.05},\"mapbox\":{\"style\":\"light\"}}},\"xaxis\":{\"anchor\":\"y\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Number Of Ratings\"}},\"yaxis\":{\"anchor\":\"x\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Sale Price\"}},\"legend\":{\"tracegroupgap\":0,\"itemsizing\":\"constant\"},\"title\":{\"text\":\"Relationship between Sale Price and Number of Ratings of iPhones 12\"}},                        {\"responsive\": true}                    ).then(function(){\n",
              "                            \n",
              "var gd = document.getElementById('09c84a70-a89b-44f2-9d8a-3884588cca4d');\n",
              "var x = new MutationObserver(function (mutations, observer) {{\n",
              "        var display = window.getComputedStyle(gd).display;\n",
              "        if (!display || display === 'none') {{\n",
              "            console.log([gd, 'removed!']);\n",
              "            Plotly.purge(gd);\n",
              "            observer.disconnect();\n",
              "        }}\n",
              "}});\n",
              "\n",
              "// Listen for the removal of the full notebook cells\n",
              "var notebookContainer = gd.closest('#notebook-container');\n",
              "if (notebookContainer) {{\n",
              "    x.observe(notebookContainer, {childList: true});\n",
              "}}\n",
              "\n",
              "// Listen for the clearing of the current output cell\n",
              "var outputEl = gd.closest('.output');\n",
              "if (outputEl) {{\n",
              "    x.observe(outputEl, {childList: true});\n",
              "}}\n",
              "\n",
              "                        })                };                            </script>        </div>\n",
              "</body>\n",
              "</html>"
            ]
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "ขี้เกียจมา plot ทีล่ะ รุ่นล่ะ\n"
      ],
      "metadata": {
        "id": "NQ1GrdHBrSFN"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "counts_all = df[\"Number Of Ratings\"]\n",
        "fig = px.bar(df,x='Product Name', y = counts_all,)\n",
        "\n",
        "fig.show()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 542
        },
        "id": "z8jXfO7yu9Sz",
        "outputId": "197ab67b-7fc8-42b5-f830-b9eca7aa4022"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/html": [
              "<html>\n",
              "<head><meta charset=\"utf-8\" /></head>\n",
              "<body>\n",
              "    <div>            <script src=\"https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG\"></script><script type=\"text/javascript\">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: \"STIX-Web\"}});}</script>                <script type=\"text/javascript\">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>\n",
              "        <script charset=\"utf-8\" src=\"https://cdn.plot.ly/plotly-2.24.1.min.js\"></script>                <div id=\"08783ca5-2f3d-4972-b321-a8a0f75af229\" class=\"plotly-graph-div\" style=\"height:525px; width:100%;\"></div>            <script type=\"text/javascript\">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById(\"08783ca5-2f3d-4972-b321-a8a0f75af229\")) {                    Plotly.newPlot(                        \"08783ca5-2f3d-4972-b321-a8a0f75af229\",                        [{\"alignmentgroup\":\"True\",\"hovertemplate\":\"Product Name=%{x}\\u003cbr\\u003eNumber Of Ratings=%{y}\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"pattern\":{\"shape\":\"\"}},\"name\":\"\",\"offsetgroup\":\"\",\"orientation\":\"v\",\"showlegend\":false,\"textposition\":\"auto\",\"x\":[\"APPLE iPhone 8 Plus (Gold, 64 GB)\",\"APPLE iPhone 8 Plus (Space Grey, 256 GB)\",\"APPLE iPhone 8 Plus (Silver, 256 GB)\",\"APPLE iPhone 8 (Silver, 256 GB)\",\"APPLE iPhone 8 (Gold, 256 GB)\",\"APPLE iPhone 8 Plus (Silver, 64 GB)\",\"APPLE iPhone 8 Plus (Space Grey, 64 GB)\",\"APPLE iPhone 8 (Space Grey, 256 GB)\",\"APPLE iPhone XS Max (Silver, 64 GB)\",\"Apple iPhone XR ((PRODUCT)RED, 128 GB) (Includes EarPods, Power Adapter)\",\"Apple iPhone XR (Black, 64 GB) (Includes EarPods, Power Adapter)\",\"Apple iPhone XR (Coral, 128 GB) (Includes EarPods, Power Adapter)\",\"Apple iPhone XR (Black, 128 GB) (Includes EarPods, Power Adapter)\",\"Apple iPhone XR (White, 128 GB) (Includes EarPods, Power Adapter)\",\"APPLE iPhone 11 Pro Max (Gold, 256 GB)\",\"APPLE iPhone 11 Pro Max (Gold, 64 GB)\",\"APPLE iPhone 11 Pro Max (Midnight Green, 256 GB)\",\"APPLE iPhone 11 Pro Max (Space Grey, 64 GB)\",\"APPLE iPhone 11 Pro (Midnight Green, 64 GB)\",\"APPLE iPhone 11 Pro (Space Grey, 512 GB)\",\"APPLE iPhone 11 Pro Max (Midnight Green, 64 GB)\",\"APPLE iPhone 11 Pro (Midnight Green, 512 GB)\",\"APPLE iPhone 11 Pro (Space Grey, 256 GB)\",\"Apple iPhone SE (White, 256 GB) (Includes EarPods, Power Adapter)\",\"APPLE iPhone 12 Pro (Silver, 512 GB)\",\"APPLE iPhone 12 Pro Max (Pacific Blue, 256 GB)\",\"APPLE iPhone 12 Mini (White, 128 GB)\",\"APPLE iPhone 12 Pro (Graphite, 256 GB)\",\"APPLE iPhone 12 Mini (White, 64 GB)\",\"APPLE iPhone 12 (White, 128 GB)\",\"APPLE iPhone 12 Pro (Graphite, 128 GB)\",\"APPLE iPhone 12 Pro Max (Graphite, 256 GB)\",\"APPLE iPhone 12 Pro Max (Graphite, 128 GB)\",\"APPLE iPhone 12 Mini (Black, 128 GB)\",\"APPLE iPhone 12 Mini (Blue, 128 GB)\",\"APPLE iPhone 12 (Black, 128 GB)\",\"APPLE iPhone 12 (Blue, 128 GB)\",\"APPLE iPhone 12 Pro Max (Silver, 128 GB)\",\"APPLE iPhone 12 Mini (Red, 64 GB)\",\"APPLE iPhone 12 Pro Max (Gold, 128 GB)\",\"APPLE iPhone 12 (Green, 128 GB)\",\"APPLE iPhone 12 Pro (Pacific Blue, 512 GB)\",\"APPLE iPhone 12 (White, 64 GB)\",\"APPLE iPhone 12 (Black, 64 GB)\",\"APPLE iPhone 12 (Red, 128 GB)\",\"APPLE iPhone 12 Mini (Black, 64 GB)\",\"APPLE iPhone 12 Pro (Pacific Blue, 128 GB)\",\"APPLE iPhone 12 Pro Max (Pacific Blue, 128 GB)\",\"APPLE iPhone 12 Pro Max (Silver, 256 GB)\",\"APPLE iPhone 12 Pro Max (Gold, 256 GB)\",\"APPLE iPhone 11 (White, 128 GB)\",\"APPLE iPhone 11 (Red, 128 GB)\",\"APPLE iPhone SE (White, 64 GB)\",\"APPLE iPhone SE (Black, 128 GB)\",\"APPLE iPhone SE (White, 128 GB)\",\"APPLE iPhone SE (Red, 128 GB)\",\"APPLE iPhone 11 (Black, 128 GB)\",\"APPLE iPhone SE (Black, 64 GB)\",\"APPLE iPhone 11 (Purple, 64 GB)\",\"APPLE iPhone 11 (White, 64 GB)\",\"APPLE iPhone 11 (Black, 64 GB)\",\"APPLE iPhone 11 (Red, 64 GB)\"],\"xaxis\":\"x\",\"y\":[3431,3431,3431,11202,11202,3431,3431,11202,1454,79512,79512,79582,79512,79512,1078,1078,1078,1078,7088,7088,1078,7088,7081,95909,542,580,740,545,740,2101,545,580,580,730,730,2101,2101,580,740,580,2092,545,2101,2092,2101,740,545,580,580,580,43707,43707,95807,95909,95807,95909,43470,95909,43470,43470,43470,43470],\"yaxis\":\"y\",\"type\":\"bar\"}],                        {\"template\":{\"data\":{\"histogram2dcontour\":[{\"type\":\"histogram2dcontour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"choropleth\":[{\"type\":\"choropleth\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"histogram2d\":[{\"type\":\"histogram2d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmap\":[{\"type\":\"heatmap\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmapgl\":[{\"type\":\"heatmapgl\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"contourcarpet\":[{\"type\":\"contourcarpet\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"contour\":[{\"type\":\"contour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"surface\":[{\"type\":\"surface\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"mesh3d\":[{\"type\":\"mesh3d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"scatter\":[{\"fillpattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2},\"type\":\"scatter\"}],\"parcoords\":[{\"type\":\"parcoords\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolargl\":[{\"type\":\"scatterpolargl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"bar\":[{\"error_x\":{\"color\":\"#2a3f5f\"},\"error_y\":{\"color\":\"#2a3f5f\"},\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"bar\"}],\"scattergeo\":[{\"type\":\"scattergeo\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolar\":[{\"type\":\"scatterpolar\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"histogram\":[{\"marker\":{\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"histogram\"}],\"scattergl\":[{\"type\":\"scattergl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatter3d\":[{\"type\":\"scatter3d\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattermapbox\":[{\"type\":\"scattermapbox\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterternary\":[{\"type\":\"scatterternary\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattercarpet\":[{\"type\":\"scattercarpet\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"carpet\":[{\"aaxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"baxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"type\":\"carpet\"}],\"table\":[{\"cells\":{\"fill\":{\"color\":\"#EBF0F8\"},\"line\":{\"color\":\"white\"}},\"header\":{\"fill\":{\"color\":\"#C8D4E3\"},\"line\":{\"color\":\"white\"}},\"type\":\"table\"}],\"barpolar\":[{\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"barpolar\"}],\"pie\":[{\"automargin\":true,\"type\":\"pie\"}]},\"layout\":{\"autotypenumbers\":\"strict\",\"colorway\":[\"#636efa\",\"#EF553B\",\"#00cc96\",\"#ab63fa\",\"#FFA15A\",\"#19d3f3\",\"#FF6692\",\"#B6E880\",\"#FF97FF\",\"#FECB52\"],\"font\":{\"color\":\"#2a3f5f\"},\"hovermode\":\"closest\",\"hoverlabel\":{\"align\":\"left\"},\"paper_bgcolor\":\"white\",\"plot_bgcolor\":\"#E5ECF6\",\"polar\":{\"bgcolor\":\"#E5ECF6\",\"angularaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"radialaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"ternary\":{\"bgcolor\":\"#E5ECF6\",\"aaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"baxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"caxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"coloraxis\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"colorscale\":{\"sequential\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"sequentialminus\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"diverging\":[[0,\"#8e0152\"],[0.1,\"#c51b7d\"],[0.2,\"#de77ae\"],[0.3,\"#f1b6da\"],[0.4,\"#fde0ef\"],[0.5,\"#f7f7f7\"],[0.6,\"#e6f5d0\"],[0.7,\"#b8e186\"],[0.8,\"#7fbc41\"],[0.9,\"#4d9221\"],[1,\"#276419\"]]},\"xaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"yaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"scene\":{\"xaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"yaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"zaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2}},\"shapedefaults\":{\"line\":{\"color\":\"#2a3f5f\"}},\"annotationdefaults\":{\"arrowcolor\":\"#2a3f5f\",\"arrowhead\":0,\"arrowwidth\":1},\"geo\":{\"bgcolor\":\"white\",\"landcolor\":\"#E5ECF6\",\"subunitcolor\":\"white\",\"showland\":true,\"showlakes\":true,\"lakecolor\":\"white\"},\"title\":{\"x\":0.05},\"mapbox\":{\"style\":\"light\"}}},\"xaxis\":{\"anchor\":\"y\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Product Name\"}},\"yaxis\":{\"anchor\":\"x\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Number Of Ratings\"}},\"legend\":{\"tracegroupgap\":0},\"margin\":{\"t\":60},\"barmode\":\"relative\"},                        {\"responsive\": true}                    ).then(function(){\n",
              "                            \n",
              "var gd = document.getElementById('08783ca5-2f3d-4972-b321-a8a0f75af229');\n",
              "var x = new MutationObserver(function (mutations, observer) {{\n",
              "        var display = window.getComputedStyle(gd).display;\n",
              "        if (!display || display === 'none') {{\n",
              "            console.log([gd, 'removed!']);\n",
              "            Plotly.purge(gd);\n",
              "            observer.disconnect();\n",
              "        }}\n",
              "}});\n",
              "\n",
              "// Listen for the removal of the full notebook cells\n",
              "var notebookContainer = gd.closest('#notebook-container');\n",
              "if (notebookContainer) {{\n",
              "    x.observe(notebookContainer, {childList: true});\n",
              "}}\n",
              "\n",
              "// Listen for the clearing of the current output cell\n",
              "var outputEl = gd.closest('.output');\n",
              "if (outputEl) {{\n",
              "    x.observe(outputEl, {childList: true});\n",
              "}}\n",
              "\n",
              "                        })                };                            </script>        </div>\n",
              "</body>\n",
              "</html>"
            ]
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "figure = px.scatter(data_frame = df, x=\"Number Of Ratings\",\n",
        "                    y=\"Sale Price\", size=\"Discount Percentage\",\n",
        "                    trendline=\"ols\",\n",
        "                    title=\"Relationship between Sale Price and Number of Ratings of iPhones\")\n",
        "figure.show()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 542
        },
        "id": "F3--PwpBvrS-",
        "outputId": "eba91392-d26b-4c0c-e5f4-05a9259cd47e"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/html": [
              "<html>\n",
              "<head><meta charset=\"utf-8\" /></head>\n",
              "<body>\n",
              "    <div>            <script src=\"https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG\"></script><script type=\"text/javascript\">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: \"STIX-Web\"}});}</script>                <script type=\"text/javascript\">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>\n",
              "        <script charset=\"utf-8\" src=\"https://cdn.plot.ly/plotly-2.24.1.min.js\"></script>                <div id=\"343ee77a-5940-4876-9e65-74bcb2fea4cd\" class=\"plotly-graph-div\" style=\"height:525px; width:100%;\"></div>            <script type=\"text/javascript\">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById(\"343ee77a-5940-4876-9e65-74bcb2fea4cd\")) {                    Plotly.newPlot(                        \"343ee77a-5940-4876-9e65-74bcb2fea4cd\",                        [{\"hovertemplate\":\"Number Of Ratings=%{x}\\u003cbr\\u003eSale Price=%{y}\\u003cbr\\u003eDiscount Percentage=%{marker.size}\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"size\":[0,0,0,0,0,0,0,0,0,20,16,20,20,20,0,0,0,0,29,15,0,15,17,18,6,6,13,6,14,10,7,6,6,13,13,10,10,6,14,6,10,6,11,11,10,14,7,6,6,6,8,8,24,22,22,22,8,24,14,14,14,14],\"sizemode\":\"area\",\"sizeref\":0.0725,\"symbol\":\"circle\"},\"mode\":\"markers\",\"name\":\"\",\"orientation\":\"v\",\"showlegend\":false,\"x\":[3431,3431,3431,11202,11202,3431,3431,11202,1454,79512,79512,79582,79512,79512,1078,1078,1078,1078,7088,7088,1078,7088,7081,95909,542,580,740,545,740,2101,545,580,580,730,730,2101,2101,580,740,580,2092,545,2101,2092,2101,740,545,580,580,580,43707,43707,95807,95909,95807,95909,43470,95909,43470,43470,43470,43470],\"xaxis\":\"x\",\"y\":[49900,84900,84900,77000,77000,49900,49900,77000,89900,41999,39999,41999,41999,41999,131900,117100,131900,117100,74999,117900,117100,117900,99900,44999,140900,130900,64900,120900,59900,75900,110900,130900,120900,64900,64900,75900,75900,120900,59900,120900,75900,140900,70900,70900,75900,59900,110900,120900,130900,130900,54999,54999,29999,34999,34999,34999,54999,29999,46999,46999,46999,46999],\"yaxis\":\"y\",\"type\":\"scatter\"},{\"hovertemplate\":\"\\u003cb\\u003eOLS trendline\\u003c\\u002fb\\u003e\\u003cbr\\u003eSale Price = -0.712783 * Number Of Ratings + 96054.8\\u003cbr\\u003eR\\u003csup\\u003e2\\u003c\\u002fsup\\u003e=0.492139\\u003cbr\\u003e\\u003cbr\\u003eNumber Of Ratings=%{x}\\u003cbr\\u003eSale Price=%{y} \\u003cb\\u003e(trend)\\u003c\\u002fb\\u003e\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"symbol\":\"circle\"},\"mode\":\"lines\",\"name\":\"\",\"showlegend\":false,\"x\":[542,545,545,545,545,580,580,580,580,580,580,580,580,730,730,740,740,740,740,1078,1078,1078,1078,1078,1454,2092,2092,2101,2101,2101,2101,2101,3431,3431,3431,3431,3431,7081,7088,7088,7088,11202,11202,11202,43470,43470,43470,43470,43470,43707,43707,79512,79512,79512,79512,79582,95807,95807,95909,95909,95909,95909],\"xaxis\":\"x\",\"y\":[95668.43493113319,95666.29658296307,95666.29658296307,95666.29658296307,95666.29658296307,95641.349187645,95641.349187645,95641.349187645,95641.349187645,95641.349187645,95641.349187645,95641.349187645,95641.349187645,95534.43177913893,95534.43177913893,95527.3039519052,95527.3039519052,95527.3039519052,95527.3039519052,95286.38339140487,95286.38339140487,95286.38339140487,95286.38339140487,95286.38339140487,95018.37708741636,94563.6217099039,94563.6217099039,94557.20666539355,94557.20666539355,94557.20666539355,94557.20666539355,94557.20666539355,93609.20564330649,93609.20564330649,93609.20564330649,93609.20564330649,93609.20564330649,91007.54870299237,91002.55922392875,91002.55922392875,91002.55922392875,88070.17109996921,88070.17109996921,88070.17109996921,65070.09818214564,65070.09818214564,65070.09818214564,65070.09818214564,65070.09818214564,64901.16867670606,64901.16867670606,39379.983266309595,39379.983266309595,39379.983266309595,39379.983266309595,39330.08847567343,27765.18878893464,27765.18878893464,27692.484951150516,27692.484951150516,27692.484951150516,27692.484951150516],\"yaxis\":\"y\",\"type\":\"scatter\"}],                        {\"template\":{\"data\":{\"histogram2dcontour\":[{\"type\":\"histogram2dcontour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"choropleth\":[{\"type\":\"choropleth\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"histogram2d\":[{\"type\":\"histogram2d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmap\":[{\"type\":\"heatmap\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmapgl\":[{\"type\":\"heatmapgl\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"contourcarpet\":[{\"type\":\"contourcarpet\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"contour\":[{\"type\":\"contour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"surface\":[{\"type\":\"surface\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"mesh3d\":[{\"type\":\"mesh3d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"scatter\":[{\"fillpattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2},\"type\":\"scatter\"}],\"parcoords\":[{\"type\":\"parcoords\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolargl\":[{\"type\":\"scatterpolargl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"bar\":[{\"error_x\":{\"color\":\"#2a3f5f\"},\"error_y\":{\"color\":\"#2a3f5f\"},\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"bar\"}],\"scattergeo\":[{\"type\":\"scattergeo\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolar\":[{\"type\":\"scatterpolar\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"histogram\":[{\"marker\":{\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"histogram\"}],\"scattergl\":[{\"type\":\"scattergl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatter3d\":[{\"type\":\"scatter3d\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattermapbox\":[{\"type\":\"scattermapbox\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterternary\":[{\"type\":\"scatterternary\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattercarpet\":[{\"type\":\"scattercarpet\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"carpet\":[{\"aaxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"baxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"type\":\"carpet\"}],\"table\":[{\"cells\":{\"fill\":{\"color\":\"#EBF0F8\"},\"line\":{\"color\":\"white\"}},\"header\":{\"fill\":{\"color\":\"#C8D4E3\"},\"line\":{\"color\":\"white\"}},\"type\":\"table\"}],\"barpolar\":[{\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"barpolar\"}],\"pie\":[{\"automargin\":true,\"type\":\"pie\"}]},\"layout\":{\"autotypenumbers\":\"strict\",\"colorway\":[\"#636efa\",\"#EF553B\",\"#00cc96\",\"#ab63fa\",\"#FFA15A\",\"#19d3f3\",\"#FF6692\",\"#B6E880\",\"#FF97FF\",\"#FECB52\"],\"font\":{\"color\":\"#2a3f5f\"},\"hovermode\":\"closest\",\"hoverlabel\":{\"align\":\"left\"},\"paper_bgcolor\":\"white\",\"plot_bgcolor\":\"#E5ECF6\",\"polar\":{\"bgcolor\":\"#E5ECF6\",\"angularaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"radialaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"ternary\":{\"bgcolor\":\"#E5ECF6\",\"aaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"baxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"caxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"coloraxis\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"colorscale\":{\"sequential\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"sequentialminus\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"diverging\":[[0,\"#8e0152\"],[0.1,\"#c51b7d\"],[0.2,\"#de77ae\"],[0.3,\"#f1b6da\"],[0.4,\"#fde0ef\"],[0.5,\"#f7f7f7\"],[0.6,\"#e6f5d0\"],[0.7,\"#b8e186\"],[0.8,\"#7fbc41\"],[0.9,\"#4d9221\"],[1,\"#276419\"]]},\"xaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"yaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"scene\":{\"xaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"yaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"zaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2}},\"shapedefaults\":{\"line\":{\"color\":\"#2a3f5f\"}},\"annotationdefaults\":{\"arrowcolor\":\"#2a3f5f\",\"arrowhead\":0,\"arrowwidth\":1},\"geo\":{\"bgcolor\":\"white\",\"landcolor\":\"#E5ECF6\",\"subunitcolor\":\"white\",\"showland\":true,\"showlakes\":true,\"lakecolor\":\"white\"},\"title\":{\"x\":0.05},\"mapbox\":{\"style\":\"light\"}}},\"xaxis\":{\"anchor\":\"y\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Number Of Ratings\"}},\"yaxis\":{\"anchor\":\"x\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Sale Price\"}},\"legend\":{\"tracegroupgap\":0,\"itemsizing\":\"constant\"},\"title\":{\"text\":\"Relationship between Sale Price and Number of Ratings of iPhones\"}},                        {\"responsive\": true}                    ).then(function(){\n",
              "                            \n",
              "var gd = document.getElementById('343ee77a-5940-4876-9e65-74bcb2fea4cd');\n",
              "var x = new MutationObserver(function (mutations, observer) {{\n",
              "        var display = window.getComputedStyle(gd).display;\n",
              "        if (!display || display === 'none') {{\n",
              "            console.log([gd, 'removed!']);\n",
              "            Plotly.purge(gd);\n",
              "            observer.disconnect();\n",
              "        }}\n",
              "}});\n",
              "\n",
              "// Listen for the removal of the full notebook cells\n",
              "var notebookContainer = gd.closest('#notebook-container');\n",
              "if (notebookContainer) {{\n",
              "    x.observe(notebookContainer, {childList: true});\n",
              "}}\n",
              "\n",
              "// Listen for the clearing of the current output cell\n",
              "var outputEl = gd.closest('.output');\n",
              "if (outputEl) {{\n",
              "    x.observe(outputEl, {childList: true});\n",
              "}}\n",
              "\n",
              "                        })                };                            </script>        </div>\n",
              "</body>\n",
              "</html>"
            ]
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "figure = px.scatter(data_frame = df, x=\"Star Rating\",\n",
        "                    y=\"Sale Price\", size=\"Discount Percentage\",\n",
        "                    trendline=\"ols\",\n",
        "                    title=\"Relationship between Sale Price and Star rating\")\n",
        "figure.show()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 542
        },
        "id": "fVQBjyyPwLYk",
        "outputId": "712094f4-2268-49d9-9f96-bc8c5d3e267d"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/html": [
              "<html>\n",
              "<head><meta charset=\"utf-8\" /></head>\n",
              "<body>\n",
              "    <div>            <script src=\"https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG\"></script><script type=\"text/javascript\">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: \"STIX-Web\"}});}</script>                <script type=\"text/javascript\">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>\n",
              "        <script charset=\"utf-8\" src=\"https://cdn.plot.ly/plotly-2.24.1.min.js\"></script>                <div id=\"f0a1103c-f0de-4789-8496-8762c1ad6edb\" class=\"plotly-graph-div\" style=\"height:525px; width:100%;\"></div>            <script type=\"text/javascript\">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById(\"f0a1103c-f0de-4789-8496-8762c1ad6edb\")) {                    Plotly.newPlot(                        \"f0a1103c-f0de-4789-8496-8762c1ad6edb\",                        [{\"hovertemplate\":\"Star Rating=%{x}\\u003cbr\\u003eSale Price=%{y}\\u003cbr\\u003eDiscount Percentage=%{marker.size}\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"size\":[0,0,0,0,0,0,0,0,0,20,16,20,20,20,0,0,0,0,29,15,0,15,17,18,6,6,13,6,14,10,7,6,6,13,13,10,10,6,14,6,10,6,11,11,10,14,7,6,6,6,8,8,24,22,22,22,8,24,14,14,14,14],\"sizemode\":\"area\",\"sizeref\":0.0725,\"symbol\":\"circle\"},\"mode\":\"markers\",\"name\":\"\",\"orientation\":\"v\",\"showlegend\":false,\"x\":[4.6,4.6,4.6,4.5,4.5,4.6,4.6,4.5,4.6,4.6,4.6,4.6,4.6,4.6,4.7,4.7,4.7,4.7,4.6,4.6,4.7,4.6,4.6,4.5,4.5,4.6,4.5,4.5,4.5,4.6,4.5,4.6,4.6,4.5,4.5,4.6,4.6,4.6,4.5,4.6,4.6,4.5,4.6,4.6,4.6,4.5,4.5,4.6,4.6,4.6,4.6,4.6,4.5,4.5,4.5,4.5,4.6,4.5,4.6,4.6,4.6,4.6],\"xaxis\":\"x\",\"y\":[49900,84900,84900,77000,77000,49900,49900,77000,89900,41999,39999,41999,41999,41999,131900,117100,131900,117100,74999,117900,117100,117900,99900,44999,140900,130900,64900,120900,59900,75900,110900,130900,120900,64900,64900,75900,75900,120900,59900,120900,75900,140900,70900,70900,75900,59900,110900,120900,130900,130900,54999,54999,29999,34999,34999,34999,54999,29999,46999,46999,46999,46999],\"yaxis\":\"y\",\"type\":\"scatter\"},{\"hovertemplate\":\"\\u003cb\\u003eOLS trendline\\u003c\\u002fb\\u003e\\u003cbr\\u003eSale Price = 176087 * Star Rating + -725665\\u003cbr\\u003eR\\u003csup\\u003e2\\u003c\\u002fsup\\u003e=0.092277\\u003cbr\\u003e\\u003cbr\\u003eStar Rating=%{x}\\u003cbr\\u003eSale Price=%{y} \\u003cb\\u003e(trend)\\u003c\\u002fb\\u003e\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"symbol\":\"circle\"},\"mode\":\"lines\",\"name\":\"\",\"showlegend\":false,\"x\":[4.5,4.5,4.5,4.5,4.5,4.5,4.5,4.5,4.5,4.5,4.5,4.5,4.5,4.5,4.5,4.5,4.5,4.5,4.5,4.5,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.6,4.7,4.7,4.7,4.7,4.7],\"xaxis\":\"x\",\"y\":[66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,66725.37962264195,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,84334.04905660404,101942.71849056624,101942.71849056624,101942.71849056624,101942.71849056624,101942.71849056624],\"yaxis\":\"y\",\"type\":\"scatter\"}],                        {\"template\":{\"data\":{\"histogram2dcontour\":[{\"type\":\"histogram2dcontour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"choropleth\":[{\"type\":\"choropleth\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"histogram2d\":[{\"type\":\"histogram2d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmap\":[{\"type\":\"heatmap\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmapgl\":[{\"type\":\"heatmapgl\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"contourcarpet\":[{\"type\":\"contourcarpet\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"contour\":[{\"type\":\"contour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"surface\":[{\"type\":\"surface\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"mesh3d\":[{\"type\":\"mesh3d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"scatter\":[{\"fillpattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2},\"type\":\"scatter\"}],\"parcoords\":[{\"type\":\"parcoords\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolargl\":[{\"type\":\"scatterpolargl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"bar\":[{\"error_x\":{\"color\":\"#2a3f5f\"},\"error_y\":{\"color\":\"#2a3f5f\"},\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"bar\"}],\"scattergeo\":[{\"type\":\"scattergeo\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolar\":[{\"type\":\"scatterpolar\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"histogram\":[{\"marker\":{\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"histogram\"}],\"scattergl\":[{\"type\":\"scattergl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatter3d\":[{\"type\":\"scatter3d\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattermapbox\":[{\"type\":\"scattermapbox\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterternary\":[{\"type\":\"scatterternary\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattercarpet\":[{\"type\":\"scattercarpet\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"carpet\":[{\"aaxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"baxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"type\":\"carpet\"}],\"table\":[{\"cells\":{\"fill\":{\"color\":\"#EBF0F8\"},\"line\":{\"color\":\"white\"}},\"header\":{\"fill\":{\"color\":\"#C8D4E3\"},\"line\":{\"color\":\"white\"}},\"type\":\"table\"}],\"barpolar\":[{\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"barpolar\"}],\"pie\":[{\"automargin\":true,\"type\":\"pie\"}]},\"layout\":{\"autotypenumbers\":\"strict\",\"colorway\":[\"#636efa\",\"#EF553B\",\"#00cc96\",\"#ab63fa\",\"#FFA15A\",\"#19d3f3\",\"#FF6692\",\"#B6E880\",\"#FF97FF\",\"#FECB52\"],\"font\":{\"color\":\"#2a3f5f\"},\"hovermode\":\"closest\",\"hoverlabel\":{\"align\":\"left\"},\"paper_bgcolor\":\"white\",\"plot_bgcolor\":\"#E5ECF6\",\"polar\":{\"bgcolor\":\"#E5ECF6\",\"angularaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"radialaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"ternary\":{\"bgcolor\":\"#E5ECF6\",\"aaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"baxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"caxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"coloraxis\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"colorscale\":{\"sequential\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"sequentialminus\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"diverging\":[[0,\"#8e0152\"],[0.1,\"#c51b7d\"],[0.2,\"#de77ae\"],[0.3,\"#f1b6da\"],[0.4,\"#fde0ef\"],[0.5,\"#f7f7f7\"],[0.6,\"#e6f5d0\"],[0.7,\"#b8e186\"],[0.8,\"#7fbc41\"],[0.9,\"#4d9221\"],[1,\"#276419\"]]},\"xaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"yaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"scene\":{\"xaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"yaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"zaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2}},\"shapedefaults\":{\"line\":{\"color\":\"#2a3f5f\"}},\"annotationdefaults\":{\"arrowcolor\":\"#2a3f5f\",\"arrowhead\":0,\"arrowwidth\":1},\"geo\":{\"bgcolor\":\"white\",\"landcolor\":\"#E5ECF6\",\"subunitcolor\":\"white\",\"showland\":true,\"showlakes\":true,\"lakecolor\":\"white\"},\"title\":{\"x\":0.05},\"mapbox\":{\"style\":\"light\"}}},\"xaxis\":{\"anchor\":\"y\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Star Rating\"}},\"yaxis\":{\"anchor\":\"x\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Sale Price\"}},\"legend\":{\"tracegroupgap\":0,\"itemsizing\":\"constant\"},\"title\":{\"text\":\"Relationship between Sale Price and Star rating\"}},                        {\"responsive\": true}                    ).then(function(){\n",
              "                            \n",
              "var gd = document.getElementById('f0a1103c-f0de-4789-8496-8762c1ad6edb');\n",
              "var x = new MutationObserver(function (mutations, observer) {{\n",
              "        var display = window.getComputedStyle(gd).display;\n",
              "        if (!display || display === 'none') {{\n",
              "            console.log([gd, 'removed!']);\n",
              "            Plotly.purge(gd);\n",
              "            observer.disconnect();\n",
              "        }}\n",
              "}});\n",
              "\n",
              "// Listen for the removal of the full notebook cells\n",
              "var notebookContainer = gd.closest('#notebook-container');\n",
              "if (notebookContainer) {{\n",
              "    x.observe(notebookContainer, {childList: true});\n",
              "}}\n",
              "\n",
              "// Listen for the clearing of the current output cell\n",
              "var outputEl = gd.closest('.output');\n",
              "if (outputEl) {{\n",
              "    x.observe(outputEl, {childList: true});\n",
              "}}\n",
              "\n",
              "                        })                };                            </script>        </div>\n",
              "</body>\n",
              "</html>"
            ]
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "คนมันดูรีวิวจริงๆ\n"
      ],
      "metadata": {
        "id": "MoZzpOBYvt-O"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "fig = px.bar(df, y='Star Rating', x='Product Name', text_auto='.2s',\n",
        "            title=\"Star rating\")\n",
        "fig.update_traces(textfont_size=12, textangle=0, textposition=\"outside\", cliponaxis=False)\n",
        "fig.show()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 542
        },
        "id": "jVJP4MxVwgLy",
        "outputId": "697af228-5ae4-4830-db14-bf065ce01948"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/html": [
              "<html>\n",
              "<head><meta charset=\"utf-8\" /></head>\n",
              "<body>\n",
              "    <div>            <script src=\"https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG\"></script><script type=\"text/javascript\">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: \"STIX-Web\"}});}</script>                <script type=\"text/javascript\">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>\n",
              "        <script charset=\"utf-8\" src=\"https://cdn.plot.ly/plotly-2.24.1.min.js\"></script>                <div id=\"b78c5bd2-fc4e-43f2-92bd-5bc0ae774568\" class=\"plotly-graph-div\" style=\"height:525px; width:100%;\"></div>            <script type=\"text/javascript\">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById(\"b78c5bd2-fc4e-43f2-92bd-5bc0ae774568\")) {                    Plotly.newPlot(                        \"b78c5bd2-fc4e-43f2-92bd-5bc0ae774568\",                        [{\"alignmentgroup\":\"True\",\"hovertemplate\":\"Product Name=%{x}\\u003cbr\\u003eStar Rating=%{y}\\u003cextra\\u003e\\u003c\\u002fextra\\u003e\",\"legendgroup\":\"\",\"marker\":{\"color\":\"#636efa\",\"pattern\":{\"shape\":\"\"}},\"name\":\"\",\"offsetgroup\":\"\",\"orientation\":\"v\",\"showlegend\":false,\"textposition\":\"outside\",\"texttemplate\":\"%{y:.2s}\",\"x\":[\"APPLE iPhone 8 Plus (Gold, 64 GB)\",\"APPLE iPhone 8 Plus (Space Grey, 256 GB)\",\"APPLE iPhone 8 Plus (Silver, 256 GB)\",\"APPLE iPhone 8 (Silver, 256 GB)\",\"APPLE iPhone 8 (Gold, 256 GB)\",\"APPLE iPhone 8 Plus (Silver, 64 GB)\",\"APPLE iPhone 8 Plus (Space Grey, 64 GB)\",\"APPLE iPhone 8 (Space Grey, 256 GB)\",\"APPLE iPhone XS Max (Silver, 64 GB)\",\"Apple iPhone XR ((PRODUCT)RED, 128 GB) (Includes EarPods, Power Adapter)\",\"Apple iPhone XR (Black, 64 GB) (Includes EarPods, Power Adapter)\",\"Apple iPhone XR (Coral, 128 GB) (Includes EarPods, Power Adapter)\",\"Apple iPhone XR (Black, 128 GB) (Includes EarPods, Power Adapter)\",\"Apple iPhone XR (White, 128 GB) (Includes EarPods, Power Adapter)\",\"APPLE iPhone 11 Pro Max (Gold, 256 GB)\",\"APPLE iPhone 11 Pro Max (Gold, 64 GB)\",\"APPLE iPhone 11 Pro Max (Midnight Green, 256 GB)\",\"APPLE iPhone 11 Pro Max (Space Grey, 64 GB)\",\"APPLE iPhone 11 Pro (Midnight Green, 64 GB)\",\"APPLE iPhone 11 Pro (Space Grey, 512 GB)\",\"APPLE iPhone 11 Pro Max (Midnight Green, 64 GB)\",\"APPLE iPhone 11 Pro (Midnight Green, 512 GB)\",\"APPLE iPhone 11 Pro (Space Grey, 256 GB)\",\"Apple iPhone SE (White, 256 GB) (Includes EarPods, Power Adapter)\",\"APPLE iPhone 12 Pro (Silver, 512 GB)\",\"APPLE iPhone 12 Pro Max (Pacific Blue, 256 GB)\",\"APPLE iPhone 12 Mini (White, 128 GB)\",\"APPLE iPhone 12 Pro (Graphite, 256 GB)\",\"APPLE iPhone 12 Mini (White, 64 GB)\",\"APPLE iPhone 12 (White, 128 GB)\",\"APPLE iPhone 12 Pro (Graphite, 128 GB)\",\"APPLE iPhone 12 Pro Max (Graphite, 256 GB)\",\"APPLE iPhone 12 Pro Max (Graphite, 128 GB)\",\"APPLE iPhone 12 Mini (Black, 128 GB)\",\"APPLE iPhone 12 Mini (Blue, 128 GB)\",\"APPLE iPhone 12 (Black, 128 GB)\",\"APPLE iPhone 12 (Blue, 128 GB)\",\"APPLE iPhone 12 Pro Max (Silver, 128 GB)\",\"APPLE iPhone 12 Mini (Red, 64 GB)\",\"APPLE iPhone 12 Pro Max (Gold, 128 GB)\",\"APPLE iPhone 12 (Green, 128 GB)\",\"APPLE iPhone 12 Pro (Pacific Blue, 512 GB)\",\"APPLE iPhone 12 (White, 64 GB)\",\"APPLE iPhone 12 (Black, 64 GB)\",\"APPLE iPhone 12 (Red, 128 GB)\",\"APPLE iPhone 12 Mini (Black, 64 GB)\",\"APPLE iPhone 12 Pro (Pacific Blue, 128 GB)\",\"APPLE iPhone 12 Pro Max (Pacific Blue, 128 GB)\",\"APPLE iPhone 12 Pro Max (Silver, 256 GB)\",\"APPLE iPhone 12 Pro Max (Gold, 256 GB)\",\"APPLE iPhone 11 (White, 128 GB)\",\"APPLE iPhone 11 (Red, 128 GB)\",\"APPLE iPhone SE (White, 64 GB)\",\"APPLE iPhone SE (Black, 128 GB)\",\"APPLE iPhone SE (White, 128 GB)\",\"APPLE iPhone SE (Red, 128 GB)\",\"APPLE iPhone 11 (Black, 128 GB)\",\"APPLE iPhone SE (Black, 64 GB)\",\"APPLE iPhone 11 (Purple, 64 GB)\",\"APPLE iPhone 11 (White, 64 GB)\",\"APPLE iPhone 11 (Black, 64 GB)\",\"APPLE iPhone 11 (Red, 64 GB)\"],\"xaxis\":\"x\",\"y\":[4.6,4.6,4.6,4.5,4.5,4.6,4.6,4.5,4.6,4.6,4.6,4.6,4.6,4.6,4.7,4.7,4.7,4.7,4.6,4.6,4.7,4.6,4.6,4.5,4.5,4.6,4.5,4.5,4.5,4.6,4.5,4.6,4.6,4.5,4.5,4.6,4.6,4.6,4.5,4.6,4.6,4.5,4.6,4.6,4.6,4.5,4.5,4.6,4.6,4.6,4.6,4.6,4.5,4.5,4.5,4.5,4.6,4.5,4.6,4.6,4.6,4.6],\"yaxis\":\"y\",\"type\":\"bar\",\"textfont\":{\"size\":12},\"cliponaxis\":false,\"textangle\":0}],                        {\"template\":{\"data\":{\"histogram2dcontour\":[{\"type\":\"histogram2dcontour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"choropleth\":[{\"type\":\"choropleth\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"histogram2d\":[{\"type\":\"histogram2d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmap\":[{\"type\":\"heatmap\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"heatmapgl\":[{\"type\":\"heatmapgl\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"contourcarpet\":[{\"type\":\"contourcarpet\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"contour\":[{\"type\":\"contour\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"surface\":[{\"type\":\"surface\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"},\"colorscale\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]]}],\"mesh3d\":[{\"type\":\"mesh3d\",\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}],\"scatter\":[{\"fillpattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2},\"type\":\"scatter\"}],\"parcoords\":[{\"type\":\"parcoords\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolargl\":[{\"type\":\"scatterpolargl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"bar\":[{\"error_x\":{\"color\":\"#2a3f5f\"},\"error_y\":{\"color\":\"#2a3f5f\"},\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"bar\"}],\"scattergeo\":[{\"type\":\"scattergeo\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterpolar\":[{\"type\":\"scatterpolar\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"histogram\":[{\"marker\":{\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"histogram\"}],\"scattergl\":[{\"type\":\"scattergl\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatter3d\":[{\"type\":\"scatter3d\",\"line\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattermapbox\":[{\"type\":\"scattermapbox\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scatterternary\":[{\"type\":\"scatterternary\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"scattercarpet\":[{\"type\":\"scattercarpet\",\"marker\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}}}],\"carpet\":[{\"aaxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"baxis\":{\"endlinecolor\":\"#2a3f5f\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"minorgridcolor\":\"white\",\"startlinecolor\":\"#2a3f5f\"},\"type\":\"carpet\"}],\"table\":[{\"cells\":{\"fill\":{\"color\":\"#EBF0F8\"},\"line\":{\"color\":\"white\"}},\"header\":{\"fill\":{\"color\":\"#C8D4E3\"},\"line\":{\"color\":\"white\"}},\"type\":\"table\"}],\"barpolar\":[{\"marker\":{\"line\":{\"color\":\"#E5ECF6\",\"width\":0.5},\"pattern\":{\"fillmode\":\"overlay\",\"size\":10,\"solidity\":0.2}},\"type\":\"barpolar\"}],\"pie\":[{\"automargin\":true,\"type\":\"pie\"}]},\"layout\":{\"autotypenumbers\":\"strict\",\"colorway\":[\"#636efa\",\"#EF553B\",\"#00cc96\",\"#ab63fa\",\"#FFA15A\",\"#19d3f3\",\"#FF6692\",\"#B6E880\",\"#FF97FF\",\"#FECB52\"],\"font\":{\"color\":\"#2a3f5f\"},\"hovermode\":\"closest\",\"hoverlabel\":{\"align\":\"left\"},\"paper_bgcolor\":\"white\",\"plot_bgcolor\":\"#E5ECF6\",\"polar\":{\"bgcolor\":\"#E5ECF6\",\"angularaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"radialaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"ternary\":{\"bgcolor\":\"#E5ECF6\",\"aaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"baxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"},\"caxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\"}},\"coloraxis\":{\"colorbar\":{\"outlinewidth\":0,\"ticks\":\"\"}},\"colorscale\":{\"sequential\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"sequentialminus\":[[0.0,\"#0d0887\"],[0.1111111111111111,\"#46039f\"],[0.2222222222222222,\"#7201a8\"],[0.3333333333333333,\"#9c179e\"],[0.4444444444444444,\"#bd3786\"],[0.5555555555555556,\"#d8576b\"],[0.6666666666666666,\"#ed7953\"],[0.7777777777777778,\"#fb9f3a\"],[0.8888888888888888,\"#fdca26\"],[1.0,\"#f0f921\"]],\"diverging\":[[0,\"#8e0152\"],[0.1,\"#c51b7d\"],[0.2,\"#de77ae\"],[0.3,\"#f1b6da\"],[0.4,\"#fde0ef\"],[0.5,\"#f7f7f7\"],[0.6,\"#e6f5d0\"],[0.7,\"#b8e186\"],[0.8,\"#7fbc41\"],[0.9,\"#4d9221\"],[1,\"#276419\"]]},\"xaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"yaxis\":{\"gridcolor\":\"white\",\"linecolor\":\"white\",\"ticks\":\"\",\"title\":{\"standoff\":15},\"zerolinecolor\":\"white\",\"automargin\":true,\"zerolinewidth\":2},\"scene\":{\"xaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"yaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2},\"zaxis\":{\"backgroundcolor\":\"#E5ECF6\",\"gridcolor\":\"white\",\"linecolor\":\"white\",\"showbackground\":true,\"ticks\":\"\",\"zerolinecolor\":\"white\",\"gridwidth\":2}},\"shapedefaults\":{\"line\":{\"color\":\"#2a3f5f\"}},\"annotationdefaults\":{\"arrowcolor\":\"#2a3f5f\",\"arrowhead\":0,\"arrowwidth\":1},\"geo\":{\"bgcolor\":\"white\",\"landcolor\":\"#E5ECF6\",\"subunitcolor\":\"white\",\"showland\":true,\"showlakes\":true,\"lakecolor\":\"white\"},\"title\":{\"x\":0.05},\"mapbox\":{\"style\":\"light\"}}},\"xaxis\":{\"anchor\":\"y\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Product Name\"}},\"yaxis\":{\"anchor\":\"x\",\"domain\":[0.0,1.0],\"title\":{\"text\":\"Star Rating\"}},\"legend\":{\"tracegroupgap\":0},\"title\":{\"text\":\"Star rating\"},\"barmode\":\"relative\"},                        {\"responsive\": true}                    ).then(function(){\n",
              "                            \n",
              "var gd = document.getElementById('b78c5bd2-fc4e-43f2-92bd-5bc0ae774568');\n",
              "var x = new MutationObserver(function (mutations, observer) {{\n",
              "        var display = window.getComputedStyle(gd).display;\n",
              "        if (!display || display === 'none') {{\n",
              "            console.log([gd, 'removed!']);\n",
              "            Plotly.purge(gd);\n",
              "            observer.disconnect();\n",
              "        }}\n",
              "}});\n",
              "\n",
              "// Listen for the removal of the full notebook cells\n",
              "var notebookContainer = gd.closest('#notebook-container');\n",
              "if (notebookContainer) {{\n",
              "    x.observe(notebookContainer, {childList: true});\n",
              "}}\n",
              "\n",
              "// Listen for the clearing of the current output cell\n",
              "var outputEl = gd.closest('.output');\n",
              "if (outputEl) {{\n",
              "    x.observe(outputEl, {childList: true});\n",
              "}}\n",
              "\n",
              "                        })                };                            </script>        </div>\n",
              "</body>\n",
              "</html>"
            ]
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "x = df['Number Of Ratings']\n",
        "y = df['Discount Percentage']\n",
        "plt.scatter(x,y)"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 447
        },
        "id": "1pa2phC5ssNQ",
        "outputId": "313dae82-ab9c-4b05-e5c1-d63ab2cfac19"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "<matplotlib.collections.PathCollection at 0x78f8d2bfcc40>"
            ]
          },
          "metadata": {},
          "execution_count": 34
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 640x480 with 1 Axes>"
            ],
            "image/png": "iVBORw0KGgoAAAANSUhEUgAAAjYAAAGdCAYAAAABhTmFAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjcuMSwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy/bCgiHAAAACXBIWXMAAA9hAAAPYQGoP6dpAAArf0lEQVR4nO3de3TU9Z3/8dckIZOkZAYTyK0ECN4wBK0iYFR0W6NcPFSs7qoLCq0HCwuuiKstrUpZq3Flj622iso5Sr0g6vkJiiIuCxKwDaBchBilouFiyWWFZiZckkDm8/uDkylDEjJJZjKTzzwf53zPMd/vO9958xllXn6/8/18HMYYIwAAAAvERboBAACAUCHYAAAAaxBsAACANQg2AADAGgQbAABgDYINAACwBsEGAABYg2ADAACskRDpBk7n8/l04MABpaamyuFwRLodAAAQBGOM6urqlJOTo7i4yF03ibpgc+DAAeXm5ka6DQAA0An79+9X//79I/b6HQo2Cxcu1MKFC7Vnzx5J0tChQ/Xwww9r3LhxkqT6+nrdd999Wrp0qRoaGjRmzBg9++yzyszMDPo1UlNTJZ0cGJfL1ZH2AABAhHi9XuXm5vo/xyPF0ZG1olasWKH4+Hide+65MsboT3/6kxYsWKBt27Zp6NChmjFjht5//30tXrxYbrdbs2bNUlxcnP785z8H3ZDX65Xb7ZbH4yHYAADQQ0TL53eHgk1r0tLStGDBAt18883q16+flixZoptvvlmS9OWXX+qCCy5QaWmpLrvssqDOFy0DAwAAghctn9+d/nZPU1OTli5dqiNHjqiwsFBbtmzR8ePHVVRU5K8ZMmSIBgwYoNLS0jbP09DQIK/XG7ABAAB0RoeDzc6dO9W7d285nU5Nnz5dy5YtU35+vqqqqpSYmKg+ffoE1GdmZqqqqqrN8xUXF8vtdvs3vjgMAAA6q8PB5vzzz9f27du1adMmzZgxQ1OmTFF5eXmnG5g7d648Ho9/279/f6fPBQAAYluHH/dOTEzUOeecI0kaPny4PvnkEz311FO65ZZb1NjYqNra2oCrNtXV1crKymrzfE6nU06ns+OdAwAAnKbLM+j4fD41NDRo+PDh6tWrl9asWeM/tmvXLu3bt0+FhYVdfRkAAIB2deiKzdy5czVu3DgNGDBAdXV1WrJkidatW6cPP/xQbrdbd955p+bMmaO0tDS5XC7dfffdKiwsDPqJKAAAgK7oULCpqanRHXfcocrKSrndbl144YX68MMPde2110qSfve73ykuLk433XRTwAR9AAAA3aHL89iEWrQ8Bx9KTT6jzRWHVFNXr4zUJI3MS1N8HOtgAQDsES2f31G3VpRtVpVVav6KclV66v37st1JmjchX2MLsiPYGQAA9onc8psxYFVZpWa8ujUg1EhSladeM17dqlVllRHqDAAAOxFswqTJZzR/Rblau8/XvG/+inI1+aLqTiAAAD0awSZMNlccanGl5lRGUqWnXpsrDnVfUwAAWI5gEyY1dW2Hms7UAQCA9hFswiQjNSmkdQAAoH0EmzAZmZembHeS2nqo26GTT0eNzEvrzrYAALAawSZM4uMcmjchX5JahJvmn+dNyGc+GwAAQohgE0ZjC7K1cPIlynIH3m7Kcidp4eRLmMcGAIAQY4K+MBtbkK1r87OYeRgAgG5AsOkG8XEOFZ6dHuk2AACwHreiAACANQg2AADAGgQbAABgDYINAACwBsEGAABYg2ADAACsQbABAADWINgAAABrEGwAAIA1CDYAAMAaBBsAAGANgg0AALAGwQYAAFiDYAMAAKxBsAEAANYg2AAAAGsQbAAAgDUINgAAwBoEGwAAYA2CDQAAsAbBBgAAWINgAwAArEGwAQAA1iDYAAAAaxBsAACANQg2AADAGgQbAABgDYINAACwBsEGAABYg2ADAACsQbABAADWINgAAABrEGwAAIA1CDYAAMAaBBsAAGANgg0AALBGh4JNcXGxRowYodTUVGVkZGjixInatWtXQM0//dM/yeFwBGzTp08PadMAAACt6VCwKSkp0cyZM7Vx40atXr1ax48f13XXXacjR44E1E2bNk2VlZX+7Yknnghp0wAAAK1J6EjxqlWrAn5evHixMjIytGXLFl111VX+/SkpKcrKygpNhwAAAEHq0ndsPB6PJCktLS1g/2uvvaa+ffuqoKBAc+fO1dGjR9s8R0NDg7xeb8AGAADQGR26YnMqn8+n2bNn64orrlBBQYF//7/+679q4MCBysnJ0Y4dO/SLX/xCu3bt0ttvv93qeYqLizV//vzOtgEAAODnMMaYzvzijBkz9MEHH+jjjz9W//7926xbu3atrrnmGu3evVtnn312i+MNDQ1qaGjw/+z1epWbmyuPxyOXy9WZ1gAAQDfzer1yu90R//zu1BWbWbNm6b333tP69evPGGokadSoUZLUZrBxOp1yOp2daQMAACBAh4KNMUZ33323li1bpnXr1ikvL6/d39m+fbskKTs7u1MNAgAABKtDwWbmzJlasmSJ3nnnHaWmpqqqqkqS5Ha7lZycrK+//lpLlizR+PHjlZ6erh07dujee+/VVVddpQsvvDAsfwAAAIBmHfqOjcPhaHX/Sy+9pKlTp2r//v2aPHmyysrKdOTIEeXm5urGG2/Ugw8+GPT9tmi5RwcAAIIXLZ/fHb4VdSa5ubkqKSnpUkMAACD0mnxGG78+qNJvvpPkUOHZ6bpscLri41q/aNFTdfpxbwAA0DOsKqvUL9/eqdqjx/37/vjRbvVJ6aXHfzJMYwvs+R4si2ACAGCxVWWVmv7q1oBQ06z26HFNf3WrVpVVRqCz8CDYAABgqSaf0W/e/bzduvkrytXk69S0dlGHYAMAgKU2VxxSlbeh3bpKT702Vxzqho7Cj2ADAIClaurqw1IbzQg2AABYKiM1KSy10YxgAwCApUbmpSnL1f6yRdnuJI3MS+uGjsKPYAMAgKXi4xz6zY+Htls3b0K+NfPZEGwAALDY2IJsPTf5EvVJ6dXi2FkpvfTc5EusmseGCfoAALDc2IJsXZufxczDAADADvFxDl1xbl9dcW7fSLcSVtyKAgAA1iDYAAAAaxBsAACANQg2AADAGgQbAABgDYINAACwBsEGAABYg2ADAACsQbABAADWINgAAABrEGwAAIA1CDYAAMAaLIIJAEAMaPIZ/WX3d/p/W7/V0cYTGjEoXVMuH6TEBLuucTiMMSbSTZzK6/XK7XbL4/HI5XJFuh0AAHq8VWWVmvPmZzra2BSw3+GQ7hqdp7nj87v8GtHy+c0VGwAALLaqrFLTX93a6jFjpOfXV0hSSMJNNLDr+hMAAPBr8hnNe+fzdusWbahQ4wlfN3QUfgQbAAAstbnikKrrGtqt8xnpldI94W+oGxBsAACwVE1dfdC1ew8dDWMn3YdgAwCApTJSk4KuHZiWEsZOug/BBgAAS43MS1NmqrPdujiHdHvhoPA31A0INgAAWCo+zqH5Nwxtt27a6Dxr5rOx408BAABaNbYgW89NvkQpifEtjjkc0s+vCs08NtGCeWwAALDc2IJsXZufFRMzDxNsAACIAfFxDo0+r59Gn9cv0q2ElV0xDQAAxDSCDQAAsAbBBgAAWINgAwAArEGwAQAA1iDYAAAAaxBsAACANQg2AADAGgQbAABgDYINAACwBsEGAABYg7WiAAA9zrHGJj36frk++7ZWrqReumv0YF15Xj/Fxzki3RoirENXbIqLizVixAilpqYqIyNDEydO1K5duwJq6uvrNXPmTKWnp6t379666aabVF1dHdKmAQCxa9rLn+iCh1fp1U37tPNvXv3564OasvjkvlVllZFuDxHWoWBTUlKimTNnauPGjVq9erWOHz+u6667TkeOHPHX3HvvvVqxYoXeeustlZSU6MCBA/rJT34S8sYBALFn2sufaHV5TavHGk/4NP3VrYSbGOcwxpjO/vL//d//KSMjQyUlJbrqqqvk8XjUr18/LVmyRDfffLMk6csvv9QFF1yg0tJSXXbZZe2e0+v1yu12y+PxyOVydbY1AIBljjU26YKHV7Vbl5maqL/MLeK2VDeLls/vLn152OPxSJLS0tIkSVu2bNHx48dVVFTkrxkyZIgGDBig0tLSVs/R0NAgr9cbsAEAcLrHVpYHVVdd16jNFYfC3A2iVaeDjc/n0+zZs3XFFVeooKBAklRVVaXExET16dMnoDYzM1NVVVWtnqe4uFhut9u/5ebmdrYlAIDF9hw8GnRtTV19GDtBNOt0sJk5c6bKysq0dOnSLjUwd+5ceTwe/7Z///4unQ8AYKdB6SlB12akJoWxE0SzTgWbWbNm6b333tNHH32k/v37+/dnZWWpsbFRtbW1AfXV1dXKyspq9VxOp1MulytgAwDgdL8anx9UXWZqokbmpYW5G0SrDgUbY4xmzZqlZcuWae3atcrLyws4Pnz4cPXq1Utr1qzx79u1a5f27dunwsLC0HQMAIhJyYnxujY/o926+TcU8MXhGNahCfpmzpypJUuW6J133lFqaqr/ezNut1vJyclyu9268847NWfOHKWlpcnlcunuu+9WYWFhUE9EAQBwJovuGNHmI9/OhDg9desPNLYgOwKdIVp06HFvh6P1BPzSSy9p6tSpkk5O0Hfffffp9ddfV0NDg8aMGaNnn322zVtRp4uWx8UAANGLmYejT7R8fndpHptwiJaBAQAAwYuWz28WwQQAANYg2AAAAGsQbAAAgDUINgAAwBoEGwAAYA2CDQAAsAbBBgAAWINgAwAArEGwAQAA1iDYAAAAaxBsAACANTq0ujcAAOi5mnxGmysOqaauXhmpSRqZl2bdwqEEGwAAYsCqskrNX1GuSk+9f1+2O0nzJuRrbEF2BDsLLW5FAQBguVVllZrx6taAUCNJVZ56zXh1q1aVVUaos9Aj2AAAYLEmn9H8FeUyrRxr3jd/RbmafK1V9DwEGwAALLa54lCLKzWnMpIqPfXaXHGo+5oKI4INAAAWq6lrO9R0pi7aEWwAALBYRmpSSOuiHcEGAACLjcxLU7Y7SW091O3QyaejRualdWdbYUOwAQDAYvFxDs2bkC9JLcJN88/zJuRbM58NwQYAAMuNLcjWwsmXKMsdeLspy52khZMvsWoeGyboAwAgBowtyNa1+VnMPAwAAOwQH+dQ4dnpkW4jrAg23SAW1uYAACAaEGzCLFbW5gAAIBrw5eEwiqW1OQAAiAYEmzCJtbU5AACIBgSbMIm1tTkAAIgGBJswibW1OQAAiAYEmzCJtbU5AACIBgSbMIm1tTkAAIgGBJswibW1OQAAiAYEmzCKpbU5AACIBkzQF2axsjYHAADRgGDTDWJhbQ4A6E4sVYO2EGwAAD0KS9XgTPiODQCgx2CpGrSHYAMA6BFYqgbBINgAAHoElqpBMAg2AIAegaVqEAyCDQCgR2CpGgSDYAMA6BFYqgbBINgAAHoElqpBMAg2AIAeg6Vq0B4m6AMA9CgsVYMzIdgAAHoclqpBWwg23aDxhE+vlO7R3kNHNTAtRbcXDlJiAncBAQAItQ5/uq5fv14TJkxQTk6OHA6Hli9fHnB86tSpcjgcAdvYsWND1W+PU7yyXEMe+kCPvP+FXi7dq0fe/0JDHvpAxSvLI90aAADW6XCwOXLkiC666CI988wzbdaMHTtWlZWV/u3111/vUpM9VfHKcj2/vkKnz+7tM9Lz6ysINwAAhFiHb0WNGzdO48aNO2ON0+lUVlZWp5uyQeMJnxZtqDhjzaINFbrvuiHclgIAIETC8om6bt06ZWRk6Pzzz9eMGTN08ODBNmsbGhrk9XoDNhu8UrqnxZWa0/nMyToAABAaIQ82Y8eO1csvv6w1a9bov/7rv1RSUqJx48apqamp1fri4mK53W7/lpubG+qWImLvoaMhrQMAAO0L+VNRt956q/+fhw0bpgsvvFBnn3221q1bp2uuuaZF/dy5czVnzhz/z16v14pwMzAtJaR1AACgfWH/csfgwYPVt29f7d69u9XjTqdTLpcrYLPB7YWD1N5cUXGOk3UAACA0wh5svv32Wx08eFDZ2bE1zXViQpymjc47Y8200Xl8cRgAgBDq8K2ow4cPB1x9qaio0Pbt25WWlqa0tDTNnz9fN910k7KysvT111/rgQce0DnnnKMxY8aEtPGeYO74k4u1LdoQ+Mh3nONkqGk+DgAAQsNhjGnn2Z1A69at0w9/+MMW+6dMmaKFCxdq4sSJ2rZtm2pra5WTk6PrrrtOjzzyiDIzM4M6v9frldvtlsfjsea2FDMPAwBsFy2f3x0ONuEWzoE51tikx1aWa8/BoxqUnqJfjc9XcmJ8SF8D6OkO15/QvW9s076/H9OAs5L1u1suVu8kVl8BcGYEmzaEa2CmvfyJVpfXtNh/bX6GFt0xImSvA/RkP/7jBu34tuVcUhf2d+ndWaMj0BGAniJagk1M3A9pK9RI0uryGk17+ZNu7giIPm2FGkna8a1XP/7jhm7uCAA6zvpgc6yxqc1Q02x1eY2ONbY+gSAQCw7Xn2gz1DTb8a1Xh+tPdFNHANA51gebx4JcaDLYOsBG976xLaR1ABAp1gebPQeDW7Ig2DrARvv+fiykdQAQKdYHm0HpwS1ZEGwdYKMBZyWHtA4AIsX6YPOrICfBC7YOsNHvbrk4pHUAECnWB5vkxHhdm59xxppr8zOYzwYxrXdSgi7sf+bHMy/s72I+GwBRz/pgI0mL7hjRZrhhHhvgpHdnjW4z3DCPDYCeImYm6JOYeRgIBjMPA+iMaJmgL6aCDQAACI9o+fyOqf8N44oNAAB2i5lgc/qyChu+kl7ZuI/v2AAAYJGY+PIwa0UBABAbrA82rBUFAEDssD7YsFYUAACxw/pgw1pRAADEDuuDDWtFAQAQO6wPNqwVBQBA7LA+2LBWFAAAscP6YCOxVhQAALEiZiboW3THCGYeBgDAcjETbKSTt6UemTgs0m0AAIAwiYlbUQAAIDYQbAAAgDUINgAAwBoEGwAAYA2CDQAAsAbBBgAAWINgAwAArEGwAQAA1iDYAAAAaxBsAACANQg2AADAGjG1VlRbGk/49ErpHu09dFQD01J0e+EgJSaQ+QAA6GliPtgUryzXog0V8pl/7Ht05ReaNjpPc8fnR64xAADQYTEdbIpXluv59RUt9vuM/PsJNwAA9Bwxe7+l8YRPiza0DDWnWrShQo0nfN3UEQAA6KqYDTavlO4JuP3UGp85WQcAAHqGmA02ew8dDWkdAACIvJgNNgPTUkJaBwAAIi9mg83thYMU5zhzTZzjZB0AAOgZYjbYJCbEadrovDPWTBudx3w2AAD0IDH9uHfzo9ynz2MT5xDz2AAA0AM5jDHtPBvUvbxer9xutzwej1wuV7e8JjMPAwDQNZH4/G5NTF+xaZaYEKc7Rw+OdBsAAKCLCDaSPEeP62eLN+uAp1457iS9OHWk3Cm9It0WAADooA7fb1m/fr0mTJignJwcORwOLV++POC4MUYPP/ywsrOzlZycrKKiIn311Veh6jfkrl6wVhf95/9oy75aVXrqtWVfrS76z//R1QvWRro1AADQQR0ONkeOHNFFF12kZ555ptXjTzzxhJ5++mk999xz2rRpk773ve9pzJgxqq+v73KzoXb1grXae/BYq8f2HjxGuAEAoIfp8K2ocePGady4ca0eM8bo97//vR588EHdcMMNkqSXX35ZmZmZWr58uW699daudRtCnqPH2ww1zfYePCbP0ePclgIAoIcI6aM/FRUVqqqqUlFRkX+f2+3WqFGjVFpa2urvNDQ0yOv1Bmzd4WeLN4e0DgAARF5Ig01VVZUkKTMzM2B/Zmam/9jpiouL5Xa7/Vtubm4oW2rTAU9wt8aCrQMAAJEX8cla5s6dK4/H49/279/fLa+b404KaR0AAIi8kAabrKwsSVJ1dXXA/urqav+x0zmdTrlcroCtO7w4dWRI6wAAQOSFNNjk5eUpKytLa9as8e/zer3atGmTCgsLQ/lSXeZO6aWB6clnrBmYnswXhwEA6EE6HGwOHz6s7du3a/v27ZJOfmF4+/bt2rdvnxwOh2bPnq3f/va3evfdd7Vz507dcccdysnJ0cSJE0PceteV3P+jNsPNwPRkldz/o27uCAAAdEWH14pat26dfvjDH7bYP2XKFC1evFjGGM2bN08vvPCCamtrdeWVV+rZZ5/VeeedF9T5I7HWBDMPAwDQNdGyVhSLYAIAgC6Lls/viD8VBQAAECoEGwAAYA2CDQAAsAbBBgAAWINgAwAArEGwAQAA1iDYAAAAaxBsAACANQg2AADAGgQbAABgDYINAACwRkKkGwAQXZp8Rn/Z/Z3e3vqtjjQ2acSgszTl8jwlJvD/QQCiH4tgAvBbVVap+978TEcamwL2OyTddVWe5o7Pj0xjAKJetHx+c8UGgKSToWb6q1tbPWYkPb++QpIINwCiGteWAajJZ/Sbd8vbrXthfYUaT/i6oSMA6ByCDQBtrjikKm99u3VG0iule8LeDwB0FsEGgGrq2g81zfYeOhrGTgCgawg2AJSRmhR07cC0lDB2AgBdQ7ABoJF5acpytR9uHJJuLxwU9n4AoLMINgAUH+fQb37c/tNOd13FfDYAoht/QwGQJI0tyNZzky/R9xLjWxxzSPo589gA6AGYxwaA39iCbF2bn8XMwwB6rJgJNo0nfHqldI/2HjqqgWkpur1wEH9RA62Ij3No9Hn9NPq8fpFuBQA6LCaCTfHKci3aUCHfKYtHPLryC00bzaV1AABsYn2wKV5Z7p8K/lQ+wxTxAADYxup7MY0nfFq0oWWoOdWiDUwRDwCALawONq+U7gm4/dQan2GKeAAAbGF1sAl26nemiAcAwA5WB5tgp35ningAAOxgdbC5vXCQ4hxnrolzMEU8AAC2sDrYJCbEadrovDPWTBvNxGMAANjC+se9mx/lPn0emziHmMcGAADLOIwx7Tw31L28Xq/cbrc8Ho9cLlfIzsvMwwAAhE+4Pr87yvorNs0SE+J05+jBkW4DAACEUcwEm4qaIxr7VIkamoyc8Q6tuudq5WV8L9JtAQCAEIqJYDN47vsB369paDL64ZPrFOeQvim+PnKNAQCAkLL+Syanh5pT+czJ4wAAwA5WB5uKmiNBLalQUXOkexoCAABhZXWwGftUSUjrAABAdLM62DQ0Bfcke7B1AAAgulkdbJzx7ayn0ME6AAAQ3awONqvuuTqkdQAAILpZHWzyMr4X1CKYzGcDAIAdrA420sl5atoKN8xjAwCAXWJigr5viq9n5mEAAGJATAQb6eTtpl2Pjo90GwAAIIysvxUFAABiR8iDzW9+8xs5HI6AbciQIaF+GQAAgBbCcitq6NCh+t///d9/vEhCzNzxAgAAERSWxJGQkKCsrKxwnBoAAKBNYfmOzVdffaWcnBwNHjxYkyZN0r59+9qsbWhokNfrDdgAAAA6I+TBZtSoUVq8eLFWrVqlhQsXqqKiQqNHj1ZdXV2r9cXFxXK73f4tNzc31C0BAIAY4TDGhHUFyNraWg0cOFBPPvmk7rzzzhbHGxoa1NDQ4P/Z6/UqNzdXHo9HLpcrnK0BAIAQ8Xq9crvdEf/8Dvu3evv06aPzzjtPu3fvbvW40+mU0+kMdxsAACAGhH0em8OHD+vrr79WdnZ2uF8KAADEuJAHm//4j/9QSUmJ9uzZo7/85S+68cYbFR8fr9tuuy3ULwUAABAg5Leivv32W9122206ePCg+vXrpyuvvFIbN25Uv379Qv1SAAAAAUIebJYuXRrqUwIAAASFtaIAAIA1CDYAAMAaBBsAAGANgg0AALAGwQYAAFiDYAMAAKxBsAEAANYg2AAAAGsQbAAAgDUINgAAwBoEGwAAYA2CDQAAsAbBBgAAWINgAwAArEGwAQAA1iDYAAAAaxBsAACANQg2AADAGgQbAABgDYINAACwBsEGAABYg2ADAACsQbABAADWINgAAABrEGwAAIA1CDYAAMAaBBsAAGANgg0AALAGwQYAAFiDYAMAAKxBsAEAANYg2AAAAGsQbAAAgDUINgAAwBoEGwAAYA2CDQAAsAbBBgAAWINgAwAArEGwAQAA1iDYAAAAaxBsAACANQg2AADAGgQbAABgDYINAACwBsEGAABYIyHSDXQ3z9Hj+tnizTpQW6/UpHj99IpBGtQ3VSPz0hQf52i73lOvHHeSXpw6Uu6UXhHo/KRjjU16bGW59hw8qkHpKfrV+HwlJ8ZHrB8AAKKJwxhjIt3Eqbxer9xutzwej1wuV0jPffWCtdp78Firx7LdSZo3IV9jC7LbrR+YnqyS+38U0t6CMe3lT7S6vKbF/mvzM7TojhHd3g8AAM3C+fndEWG7FfXMM89o0KBBSkpK0qhRo7R58+ZwvVRQzhRqJKnSU68Zr27VqrLKduv3HjymqxesDUufbWkr1EjS6vIaTXv5k27tBwCAaBSWYPPGG29ozpw5mjdvnrZu3aqLLrpIY8aMUU1N6x/M4eY5evyMoaaZkTR/RbkOHW5st37vwWPyHD0eog7P7FhjU5uhptnq8hoda2zqln4AAIhWYQk2Tz75pKZNm6af/vSnys/P13PPPaeUlBS9+OKLLWobGhrk9XoDtlD72eLgrxZVeup16wt/Cfl5u+KxleUhrQMAwFYhDzaNjY3asmWLioqK/vEicXEqKipSaWlpi/ri4mK53W7/lpubG+qWdMBT36H6mrrGsJy3s/YcPBrSOgAAbBXyYPPdd9+pqalJmZmZAfszMzNVVVXVon7u3LnyeDz+bf/+/aFuSTnupA7VZ6QmhuW8nTUoPSWkdQAA2Cri89g4nU65XK6ALdRenDoy6Npsd5KW3nV5yM/bFb8anx/SOgAAbBXyYNO3b1/Fx8eruro6YH91dbWysrJC/XJBcaf00sD05HbrHJLmTchXWu/EdusHpid323w2yYnxujY/44w11+ZnMJ8NACDmhTzYJCYmavjw4VqzZo1/n8/n05o1a1RYWBjqlwtayf0/OmNYyXYnaeHkS/zz2JypPhLz2Cy6Y0Sb4YZ5bAAAOCksE/S98cYbmjJlip5//nmNHDlSv//97/Xmm2/qyy+/bPHdm9OFe4IfZh4GACD0omWCvrDNPPzHP/5RCxYsUFVVlX7wgx/o6aef1qhRo9r9vWgZGAAAELxo+fyOqSUVAABAeETL53fEn4oCAAAIFYINAACwBsEGAABYg2ADAACsQbABAADWINgAAABrEGwAAIA1CDYAAMAaCZFu4HTN8wV6vd4IdwIAAILV/Lkd6Xl/oy7Y1NXVSZJyc3Mj3AkAAOiouro6ud3uiL1+1C2p4PP5dODAAaWmpsrhaLkoZUd5vV7l5uZq//79LNHQzRj7yGDcI4exjxzGPjJOHffU1FTV1dUpJydHcXGR+6ZL1F2xiYuLU//+/UN+XpfLxb/sEcLYRwbjHjmMfeQw9pHRPO6RvFLTjC8PAwAAaxBsAACANawPNk6nU/PmzZPT6Yx0KzGHsY8Mxj1yGPvIYewjIxrHPeq+PAwAANBZ1l+xAQAAsYNgAwAArEGwAQAA1iDYAAAAaxBsAACANawPNs8884wGDRqkpKQkjRo1Sps3b450S1GruLhYI0aMUGpqqjIyMjRx4kTt2rUroKa+vl4zZ85Uenq6evfurZtuuknV1dUBNfv27dP111+vlJQUZWRk6P7779eJEycCatatW6dLLrlETqdT55xzjhYvXtyin1h97x5//HE5HA7Nnj3bv49xD5+//e1vmjx5stLT05WcnKxhw4bp008/9R83xujhhx9Wdna2kpOTVVRUpK+++irgHIcOHdKkSZPkcrnUp08f3XnnnTp8+HBAzY4dOzR69GglJSUpNzdXTzzxRIte3nrrLQ0ZMkRJSUkaNmyYVq5cGZ4/dBRoamrSQw89pLy8PCUnJ+vss8/WI488ErCAImPfdevXr9eECROUk5Mjh8Oh5cuXBxyPpjEOppegGIstXbrUJCYmmhdffNF8/vnnZtq0aaZPnz6muro60q1FpTFjxpiXXnrJlJWVme3bt5vx48ebAQMGmMOHD/trpk+fbnJzc82aNWvMp59+ai677DJz+eWX+4+fOHHCFBQUmKKiIrNt2zazcuVK07dvXzN37lx/zTfffGNSUlLMnDlzTHl5ufnDH/5g4uPjzapVq/w1sfrebd682QwaNMhceOGF5p577vHvZ9zD49ChQ2bgwIFm6tSpZtOmTeabb74xH374odm9e7e/5vHHHzdut9ssX77cfPbZZ+bHP/6xycvLM8eOHfPXjB071lx00UVm48aNZsOGDeacc84xt912m/+4x+MxmZmZZtKkSaasrMy8/vrrJjk52Tz//PP+mj//+c8mPj7ePPHEE6a8vNw8+OCDplevXmbnzp3dMxjd7NFHHzXp6enmvffeMxUVFeatt94yvXv3Nk899ZS/hrHvupUrV5pf//rX5u233zaSzLJlywKOR9MYB9NLMKwONiNHjjQzZ870/9zU1GRycnJMcXFxBLvqOWpqaowkU1JSYowxpra21vTq1cu89dZb/povvvjCSDKlpaXGmJP/EcXFxZmqqip/zcKFC43L5TINDQ3GGGMeeOABM3To0IDXuuWWW8yYMWP8P8fie1dXV2fOPfdcs3r1anP11Vf7gw3jHj6/+MUvzJVXXtnmcZ/PZ7KyssyCBQv8+2pra43T6TSvv/66McaY8vJyI8l88skn/poPPvjAOBwO87e//c0YY8yzzz5rzjrrLP970fza559/vv/nf/mXfzHXX399wOuPGjXK/PznP+/aHzJKXX/99eZnP/tZwL6f/OQnZtKkScYYxj4cTg820TTGwfQSLGtvRTU2NmrLli0qKiry74uLi1NRUZFKS0sj2FnP4fF4JElpaWmSpC1btuj48eMBYzpkyBANGDDAP6alpaUaNmyYMjMz/TVjxoyR1+vV559/7q859RzNNc3niNX3bubMmbr++utbjA3jHj7vvvuuLr30Uv3zP/+zMjIydPHFF2vRokX+4xUVFaqqqgoYE7fbrVGjRgWMfZ8+fXTppZf6a4qKihQXF6dNmzb5a6666iolJib6a8aMGaNdu3bp73//u7/mTO+PbS6//HKtWbNGf/3rXyVJn332mT7++GONGzdOEmPfHaJpjIPpJVjWBpvvvvtOTU1NAX/RS1JmZqaqqqoi1FXP4fP5NHv2bF1xxRUqKCiQJFVVVSkxMVF9+vQJqD11TKuqqlod8+ZjZ6rxer06duxYTL53S5cu1datW1VcXNziGOMePt98840WLlyoc889Vx9++KFmzJihf//3f9ef/vQnSf8YuzONSVVVlTIyMgKOJyQkKC0tLSTvj61j/8tf/lK33nqrhgwZol69euniiy/W7NmzNWnSJEmMfXeIpjEOppdgJXSoGjFj5syZKisr08cffxzpVqy3f/9+3XPPPVq9erWSkpIi3U5M8fl8uvTSS/XYY49Jki6++GKVlZXpueee05QpUyLcnd3efPNNvfbaa1qyZImGDh2q7du3a/bs2crJyWHs0SXWXrHp27ev4uPjWzw5Ul1draysrAh11TPMmjVL7733nj766CP179/fvz8rK0uNjY2qra0NqD91TLOyslod8+ZjZ6pxuVxKTk6Oufduy5Ytqqmp0SWXXKKEhAQlJCSopKRETz/9tBISEpSZmcm4h0l2drby8/MD9l1wwQXat2+fpH+M3ZnGJCsrSzU1NQHHT5w4oUOHDoXk/bF17O+//37/VZthw4bp9ttv17333uu/asnYh180jXEwvQTL2mCTmJio4cOHa82aNf59Pp9Pa9asUWFhYQQ7i17GGM2aNUvLli3T2rVrlZeXF3B8+PDh6tWrV8CY7tq1S/v27fOPaWFhoXbu3BnwH8Lq1avlcrn8HyCFhYUB52iuaT5HrL1311xzjXbu3Knt27f7t0svvVSTJk3y/zPjHh5XXHFFiykN/vrXv2rgwIGSpLy8PGVlZQWMidfr1aZNmwLGvra2Vlu2bPHXrF27Vj6fT6NGjfLXrF+/XsePH/fXrF69Wueff77OOussf82Z3h/bHD16VHFxgR9B8fHx8vl8khj77hBNYxxML0Hr0FeNe5ilS5cap9NpFi9ebMrLy81dd91l+vTpE/DkCP5hxowZxu12m3Xr1pnKykr/dvToUX/N9OnTzYABA8zatWvNp59+agoLC01hYaH/ePNjx9ddd53Zvn27WbVqlenXr1+rjx3ff//95osvvjDPPPNMq48dx/J7d+pTUcYw7uGyefNmk5CQYB599FHz1Vdfmddee82kpKSYV1991V/z+OOPmz59+ph33nnH7Nixw9xwww2tPg578cUXm02bNpmPP/7YnHvuuQGPw9bW1prMzExz++23m7KyMrN06VKTkpLS4nHYhIQE89///d/miy++MPPmzbPmkePWTJkyxXz/+9/3P+799ttvm759+5oHHnjAX8PYd11dXZ3Ztm2b2bZtm5FknnzySbNt2zazd+9eY0x0jXEwvQTD6mBjjDF/+MMfzIABA0xiYqIZOXKk2bhxY6RbilqSWt1eeuklf82xY8fMv/3bv5mzzjrLpKSkmBtvvNFUVlYGnGfPnj1m3LhxJjk52fTt29fcd9995vjx4wE1H330kfnBD35gEhMTzeDBgwNeo1ksv3enBxvGPXxWrFhhCgoKjNPpNEOGDDEvvPBCwHGfz2ceeughk5mZaZxOp7nmmmvMrl27AmoOHjxobrvtNtO7d2/jcrnMT3/6U1NXVxdQ89lnn5krr7zSOJ1O8/3vf988/vjjLXp58803zXnnnWcSExPN0KFDzfvvvx/6P3CU8Hq95p577jEDBgwwSUlJZvDgwebXv/51wCPDjH3XffTRR63+vT5lyhRjTHSNcTC9BMNhzCnTPAIAAPRg1n7HBgAAxB6CDQAAsAbBBgAAWINgAwAArEGwAQAA1iDYAAAAaxBsAACANQg2AADAGgQbAABgDYINAACwBsEGAABY4/8DjUEfT76aZnoAAAAASUVORK5CYII=\n"
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "x=np.array(x)\n",
        "y=np.array(y)\n",
        "x=x.reshape(-1,1)"
      ],
      "metadata": {
        "id": "RZovtf_CtqLz"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "model=LinearRegression()\n",
        "model.fit(x,y)\n",
        "model.score(x,y)"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "Slb26RfFt6fz",
        "outputId": "0df7e3ef-c5c7-40d0-9770-fdf449534b60"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "0.4689880957449162"
            ]
          },
          "metadata": {},
          "execution_count": 41
        }
      ]
    }
  ]
}
