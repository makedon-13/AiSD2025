#include <iostream>
#include <vector>
#include <map>
#include <string>

using namespace std;

// Состояния вершины
enum VertexState {
    UNDISCOVERED,
    DISCOVERED,
    PROCESSED
};

class Graph {
private:
    int vertices; // Количество вершин
    vector<vector<int>> adjList; // Список смежности
    vector<VertexState> state; // Состояние вершин
    vector<int> parent; // Родительские вершины
    vector<int> entryTime; // Время входа
    vector<int> exitTime; // Время выхода
    int time; // Глобальное время

public:
    Graph(int n) : vertices(n), adjList(n), state(n, UNDISCOVERED), 
                   parent(n, -1), entryTime(n, 0), exitTime(n, 0), time(0) {}

    // Добавление ребра
    void addEdge(int u, int v) {
        adjList[u].push_back(v);
        // Для неориентированного графа раскомментируйте следующую строку:
        // adjList[v].push_back(u);
    }

    // Основная функция DFS
    void DFS(int u) {
        // Помечаем вершину как обнаруженную
        state[u] = DISCOVERED;
        
        // Обрабатываем вершину (здесь просто выводим)
        processVertex(u);
        
        // Увеличиваем время и записываем время входа
        time++;
        entryTime[u] = time;
        
        // Обрабатываем все смежные вершины
        for (int v : adjList[u]) {
            // Обрабатываем ребро (здесь просто выводим)
            processEdge(u, v);
            
            if (state[v] == UNDISCOVERED) {
                parent[v] = u;
                DFS(v);
            }
        }
        
        // Помечаем вершину как обработанную
        state[u] = PROCESSED;
        
        // Записываем время выхода и увеличиваем время
        exitTime[u] = time;
        time++;
    }

    // Запуск DFS для всего графа (для несвязных графов)
    void startDFS() {
        time = 0;
        for (int i = 0; i < vertices; i++) {
            if (state[i] == UNDISCOVERED) {
                DFS(i);
            }
        }
    }

private:
    // Обработка вершины
    void processVertex(int u) {
        cout << "Обрабатываем вершину: " << u << endl;
    }

    // Обработка ребра
    void processEdge(int u, int v) {
        string edgeType;
        
        if (state[v] == UNDISCOVERED) {
            edgeType = "Древесное ребро";
        } else if (state[v] == DISCOVERED && parent[u] != v) {
            edgeType = "Обратное ребро";
        } else {
            edgeType = "Прямое/Поперечное ребро";
        }
        
        cout << "Обрабатываем ребро (" << u << " -> " << v << "): " << edgeType << endl;
    }

public:
    // Вспомогательные функции для получения информации
    void printDFSInfo() {
        cout << "\n=== Информация о DFS обходе ===" << endl;
        for (int i = 0; i < vertices; i++) {
            cout << "Вершина " << i << ": ";
            cout << "вход=" << entryTime[i] << ", выход=" << exitTime[i];
            cout << ", родитель=" << parent[i] << endl;
        }
    }

    // Получение состояния вершины в виде строки
    string getStateString(int vertex) {
        switch(state[vertex]) {
            case UNDISCOVERED: return "Не обнаружена";
            case DISCOVERED: return "Обнаружена";
            case PROCESSED: return "Обработана";
            default: return "Неизвестно";
        }
    }
};
