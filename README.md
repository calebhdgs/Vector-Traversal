# Vector-Traversal

This program is intended to find the shortest possible route between two songs. However, it needs to be changed slightly to work and is not yet able to find the best route, only the first one. The method that does all of the work is the find_transitions method. It is given the current vector, an end vector and a list of all other vectors. The method then filters out transitions if they are too far away, and if they are farther away from the end vector.
```
import scipy.spatial.distance as dist

def euclideanDistance(vec1, vec2):
    euclid = dist.euclidean(vec1, vec2)
    print "Vectors 1 and 2"
    print vec1
    print vec2
    print "Euclidian Distance: "
    print euclid
    print "\n"
    return euclid
    #sum = 0
    #index = 0
    #while index < len(vec1) and index < len(vec2):
    #    sum += (vec1[index]-vec2[index])**2
    #    index += 1
    #return (sum)**0.5

def find_Transitions(vecList, startVec, endVec, transitionLevel):
    possible_Transitions = []

    #case: startVec is also endVec
    #result: program is done. return startVec
    if euclideanDistance(startVec, endVec) == 0.0:
        return endVec
        
    #case: no possible transitions
    #result: return null list
    elif vecList == []:
        return None
        
    #case: possible transitions
    #result: iterate through to find smooth transitions
    else:
        for x in vecList:
            possibleStep = euclideanDistance(startVec, x)
            #case: smooth transition found
            #result: see if transition is getting closer to endVec
            if possibleStep <= transitionLevel:
                stepToFinish = euclideanDistance(x, endVec)
                beginningToFinish = euclideanDistance(startVec, endVec)
                #case: smooth transition is getting closer to endVec
                #result: add transition to list of possible_Transitions
                if stepToFinish <= beginningToFinish:
                    possible_Transitions.append(x)
                    
        #case: all good transitions found
        #result: iterate through all possible transitions
        for step in possible_Transitions:
            smallerVecList = possible_Transitions
            smallerVecList.remove(step)
            print "Current vector: "
            print step
            print "All possible transitions: "
            print smallerVecList
            result = find_Transitions(possible_Transitions, step, endVec, transitionLe
            #case: full path from startVec to endVec has been found using smooth trans
            #result: append startVec to the front of the list returned by find_Transit
            if result != None:
                return [startVec].extend(result)

def main():
    vec1 = [0,0,0,0,0,0,0,0,0,0,0,0]
    vec2 = [5,5,5,5,5,5,5,5,5,5,5,5]
    vec3 = [10,10,10,10,10,10,10,10,10,10,10,10]
    vec4 = [15,15,15,15,15,15,15,15,15,15,15,15]

    smooth_Transition_Level = 500

    answer = find_Transitions([vec2, vec3, vec4], vec1, vec4, smooth_Transition_Level)
    print answer
    if answer == None:
        print "no answer found"
        print answer
    else:
        print "\nfound the answer\n"
        print answer

main()



```
