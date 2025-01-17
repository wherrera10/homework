using Plots, DSP


# a single, regular game of life, optimized for speed
function step_regular(GoL, Mfilt)

    # 2D kernel to update cells        
    Mfilt = [true true  true;
             true false true;
             true true  true]

    # Perform 2D FFT-based convolution
    convGoL = DSP.conv(GoL, Mfilt)
    lives2 = convGoL .== 2
    lives3 = convGoL .== 3

    # Keep only cells with 2 (or 3) neighbours alive
    # Make new cells if neighbours are 3
    twoLiveNeig = (GoL .&& lives2[2:end-1, 2:end-1])
    GoL = twoLiveNeig .|| lives3[2:end-1, 2:end-1]
    
    return(GoL)
end


# main Game of life function loop
function runGoL_default(GoL; runs=100,  sleepTime=0.02, safeToDisk=false, showOnConsole=true)

    # Simulate the game
    for i_gen = 1:runs

        GoL = step_regular(GoL, Mfilt)
          
        if showOnConsole
            plot(heatmap(GoL), show=true, reuse=true)
            sleep(sleepTime)
        end
    end

    return(GoL)
end


# Make a simulation grid
function initiate_grid(grid_size_width=384, grid_size_height=384)
    rand(Bool, grid_size_width, grid_size_height)
end


# start a random map
function start(GoL=nothing, runs=100, grid_size_width=384, grid_size_height=384; sleepTime=0.02)
    grid = initiate_grid(grid_size_width, grid_size_height)
    runGoL_default(grid, runs=runs, sleepTime=sleepTime)
end


# continue last run
#res = runGoL(res)
