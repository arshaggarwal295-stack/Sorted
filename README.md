# Sorted
## WAP for Quick sort and plot a graph
import matplotlib.pyplot as plt
import matplotlib.animation as animation

# Quick Sort with visualization support
def partition(arr, low, high, states):
    pivot = arr[high]
    i = low - 1

    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
            states.append(arr.copy())

    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    states.append(arr.copy())
    return i + 1

def quick_sort(arr, low, high, states):
    if low < high:
        pi = partition(arr, low, high, states)
        quick_sort(arr, low, pi - 1, states)
        quick_sort(arr, pi + 1, high, states)

# Initial setup
arr = [10, 7, 8, 9, 1, 5]
states = [arr.copy()]
quick_sort(arr, 0, len(arr) - 1, states)

# Plotting setup
fig, ax = plt.subplots()
bar_rects = ax.bar(range(len(arr)), states[0], align="edge")
ax.set_title("Quick Sort Visualization")
ax.set_xlabel("Index")
ax.set_ylabel("Value")
ax.set_ylim(0, max(arr) + 1)

def update_plot(frame):
    for rect, val in zip(bar_rects, states[frame]):
        rect.set_height(val)
    return bar_rects

ani = animation.FuncAnimation(fig, update_plot, frames=len(states), interval=500, repeat=False)
plt.show()

##WAP for Heap sort and plot a graph

import matplotlib.pyplot as plt
import matplotlib.animation as animation

# Function to heapify a subtree rooted at index i
def heapify(arr, n, i, states):
    largest = i
    l = 2 * i + 1     # left = 2*i + 1
    r = 2 * i + 2     # right = 2*i + 2

    if l < n and arr[l] > arr[largest]:
        largest = l

    if r < n and arr[r] > arr[largest]:
        largest = r

    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        states.append(arr.copy())
        heapify(arr, n, largest, states)

# Main function to sort an array of given size
def heap_sort(arr, states):
    n = len(arr)

    # Build a maxheap.
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i, states)

    # One by one extract elements
    for i in range(n - 1, 0, -1):
        arr[i], arr[0] = arr[0], arr[i]
        states.append(arr.copy())
        heapify(arr, i, 0, states)

# Visualization
def visualize_sorting(arr, states):
    fig, ax = plt.subplots()
    bar_rects = ax.bar(range(len(arr)), states[0], align="edge")
    ax.set_title("Heap Sort Visualization")
    ax.set_xlabel("Index")
    ax.set_ylabel("Value")
    ax.set_ylim(0, max(arr) + 1)

    def update_plot(frame):
        for rect, val in zip(bar_rects, states[frame]):
            rect.set_height(val)
        return bar_rects

    ani = animation.FuncAnimation(fig, update_plot, frames=len(states), interval=500, repeat=False)
    plt.show()

if __name__ == "__main__":
    arr = [10, 3, 76, 34, 23, 32]
    states = [arr.copy()]
    heap_sort(arr, states)
    visualize_sorting(arr, states)
