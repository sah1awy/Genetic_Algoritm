#include <iostream>
#include <vector>
#include <string>
#include <cstdlib>
#include <ctime>
#include<algorithm>

using namespace std;

const string TARGET = "HELLO WORLD";
const string VALID_CHARACTERS = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz ";

const int POPULATION_SIZE = 1000;
const double MUTATION_RATE = 0.01;

string generateRandomString(int length) {
    string randomString;
    for (int i = 0; i < length; ++i) {
        int randomIndex = rand() % VALID_CHARACTERS.size();
        randomString += VALID_CHARACTERS[randomIndex];
    }
    return randomString;
}

double fitness(string candidate) {
    double score = 0;
    for (int i = 0; i < candidate.size(); ++i) {
        if (candidate[i] == TARGET[i]) {
            score++;
        }
    }
    return score / TARGET.size();
}

string crossover(string parent1, string parent2) {
    string child = parent1;
    int midpoint = rand() % parent1.size();
    for (int i = midpoint; i < parent1.size(); ++i) {
        child[i] = parent2[i];
    }
    return child;
}

void mutate(string& individual) {
    for (int i = 0; i < individual.size(); ++i) {
        if (rand() / (double)RAND_MAX < MUTATION_RATE) {
            int randomIndex = rand() % VALID_CHARACTERS.size();
            individual[i] = VALID_CHARACTERS[randomIndex];
        }
    }
}

int main() {
    srand(time(0));

    // Initialize population
    vector<string> population;
    for (int i = 0; i < POPULATION_SIZE; ++i) {
        population.push_back(generateRandomString(TARGET.size()));
    }

    int generation = 0;
    while (true) {
        // Evaluate fitness
        vector<pair<double, string>> fitnessScores;
        for (const auto& individual : population) {
            fitnessScores.push_back({ fitness(individual), individual });
        }
        sort(fitnessScores.rbegin(), fitnessScores.rend());

        // Check for solution
        if (fitnessScores[0].second == TARGET) {
            cout << "Solution found in generation " << generation << ": " << fitnessScores[0].second << endl;
            break;
        }

        // Selection and reproduction
        vector<string> newPopulation;
        for (int i = 0; i < POPULATION_SIZE; ++i) {
            int index1 = rand() % (POPULATION_SIZE / 2);
            int index2 = rand() % (POPULATION_SIZE / 2);
            string child = crossover(fitnessScores[index1].second, fitnessScores[index2].second);
            mutate(child);
            newPopulation.push_back(child);
        }
        population = newPopulation;
        generation++;
    }

    return 0;
}
