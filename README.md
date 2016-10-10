# elixir_map_reduce
Map reduce implementation in Elixir with scalable mappers and reducers

# Progress

I'm working on it! If you're interested in this tutorial, send me a note to hurry up ;)

# Introduction

I have searched for map/reduce implementation in Elixir and have found a couple of versions. These m/r versions create one process per emitter and then use a single process for reducing (all reduction messages received by a single process).

In this tutorial I will create n emitters, and m reducers. Anyways, I think there should be at least one reducer per reduction key (possibly more) which then is accumulated by a final process. Also, it doesn't make a lot of sense to create more emitters processes than reducers can keep up with. 

# Considerations

I won't try to implement every general case, but consider specific cases.

An initial collection will be broken into parts. Each part will be given to a emitter process.

A reducer process will be created for each matching reduction pattern

This will require distributing the <pid> for each reduction matcher to the emitters (or some sort of lookup / dispatch).

When all data is emitted, a final end-signal will be emitted to each reducer which will trigger them to send their reudctions to the final accumulator.

A m/r implemented like this will require tuning for the dataset, but I hope to implement enough controls to make it sensible.

