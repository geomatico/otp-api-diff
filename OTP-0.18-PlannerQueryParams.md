# OTP 0.18 Planner Query Parameters

From https://github.com/opentripplanner/OpenTripPlanner/blob/master/src/main/java/org/opentripplanner/api/common/RoutingResource.java (@QueryParam):


## fromPlace (String)

The start location -- either latitude, longitude pair in degrees or a Vertex
label. For example, <code>40.714476,-74.005966</code> or
<code>mtanyctsubway_A27_S</code>.


## toPlace (String)

The end location (see fromPlace for format).


## intermediatePlaces (List<String>)

An ordered list of intermediate locations to be visited (see the fromPlace for format).
Parameter can be specified multiple times.


## date (String)

The date that the trip should depart (or arrive, for requests where arriveBy is true).


## time (String)

The time that the trip should depart (or arrive, for requests where arriveBy is true).


## arriveBy (Boolean)

Whether the trip should depart or arrive at the specified date and time.


## wheelchair (Boolean)

Whether the trip must be wheelchair accessible.


## maxWalkDistance (Double)

The maximum distance (in meters) the user is willing to walk. Defaults to unlimited.


## maxPreTransitTime (Integer)

The maximum time (in seconds) of pre-transit travel when using drive-to-transit (park and
ride or kiss and ride). Defaults to unlimited.


## walkReluctance (Double)

A multiplier for how bad walking is, compared to being in transit for equal lengths of time.
Defaults to 2. Empirically, values between 10 and 20 seem to correspond well to the concept
of not wanting to walk too much without asking for totally ridiculous itineraries, but this
observation should in no way be taken as scientific or definitive. Your mileage may vary.


## waitReluctance (Double)

How much worse is waiting for a transit vehicle than being on a transit vehicle, as a
multiplier. The default value treats wait and on-vehicle time as the same.

It may be tempting to set this higher than walkReluctance (as studies often find this kind of
preferences among riders) but the planner will take this literally and walk down a transit
line to avoid waiting at a stop. This used to be set less than 1 (0.95) which would make
waiting offboard preferable to waiting onboard in an interlined trip. That is also
undesirable.

If we only tried the shortest possible transfer at each stop to neighboring stop patterns,
this problem could disappear.


## waitAtBeginningFactor (Double)

How much less bad is waiting at the beginning of the trip (replaces waitReluctance)


## walkSpeed (Double)

The user's walking speed in meters/second. Defaults to approximately 3 MPH.


## bikeSpeed (Double)

The user's biking speed in meters/second. Defaults to approximately 11 MPH, or 9.5 for bikeshare.


## bikeSwitchTime (Integer)

The time it takes the user to fetch their bike and park it again in seconds.
Defaults to 0.


## bikeSwitchCost (Integer)

The cost of the user fetching their bike and parking it again.
Defaults to 0.


## triangleSafetyFactor (Double)

For bike triangle routing, how much safety matters (range 0-1).


## triangleSlopeFactor (Double)

For bike triangle routing, how much slope matters (range 0-1).


## triangleTimeFactor (Double)

For bike triangle routing, how much time matters (range 0-1).


## optimize (OptimizeType)

The set of characteristics that the user wants to optimize for. @See OptimizeType


## mode (QualifiedModeSet)

The set of modes that a user is willing to use, with qualifiers stating whether vehicles
should be parked, rented, etc.


## minTransferTime (Integer)

The minimum time, in seconds, between successive trips on different vehicles.
This is designed to allow for imperfect schedule adherence.  This is a minimum;
transfers over longer distances might use a longer time.


## numItineraries (Integer)

The maximum number of possible itineraries to return.


## preferredRoutes (String)

The list of preferred routes. The format is agency_[routename][_routeid],
so TriMet_100 (100 is route short name)
or Trimet__42 (two underscores, 42 is the route internal ID).


## otherThanPreferredRoutesPenalty (Integer)

Penalty added for using every route that is not preferred if user set any route as preferred,
i.e. number of seconds that we are willing to wait for preferred route.


## preferredAgencies (String)

The comma-separated list of preferred agencies.


## unpreferredRoutes (String)

The list of unpreferred routes. The format is agency_[routename][_routeid],
so TriMet_100 (100 is route short name) or Trimet__42 (two
underscores, 42 is the route internal ID).


## unpreferredAgencies (String)

The comma-separated list of unpreferred agencies.


## showIntermediateStops (Boolean)

Whether intermediate stops -- those that the itinerary passes in a vehicle, but
does not board or alight at -- should be returned in the response.  For example,
on a Q train trip from Prospect Park to DeKalb Avenue, whether 7th Avenue and
Atlantic Avenue should be included.


## walkBoardCost (Integer)

Prevents unnecessary transfers by adding a cost for boarding a vehicle. This is the cost that
is used when boarding while walking.


## bikeBoardCost (Integer)

Prevents unnecessary transfers by adding a cost for boarding a vehicle. This is the cost that
is used when boarding while cycling. This is usually higher that walkBoardCost.


## bannedRoutes (String)

The comma-separated list of banned routes. The format is agency_[routename][_routeid],
so TriMet_100 (100 is route short name) or Trimet__42
(two underscores, 42 is the route internal ID).


## bannedAgencies (String)
    
The comma-separated list of banned agencies.


## bannedTrips (String)

The comma-separated list of banned trips.  The format is agency_trip[:stop*], so:
TriMet_24601 or TriMet_24601:0:1:2:17:18:19


## bannedStops (String)

A comma-separated list of banned stops. A stop is banned by ignoring its
pre-board and pre-alight edges. This means the stop will be reachable via the
street network. Also, it is still possible to travel through the stop. Just
boarding and alighting is prohibited.
The format is agencyId_stopId, so: TriMet_2107


## bannedStopsHard (String)

A comma-separated list of banned stops. A stop is banned by ignoring its
pre-board and pre-alight edges. This means the stop will be reachable via the
street network. It is not possible to travel through the stop.
For example, this parameter can be used when a train station is destroyed, such
that no trains can drive through the station anymore.
The format is agencyId_stopId, so: TriMet_2107


## transferPenalty (Integer)

An additional penalty added to boardings after the first.  The value is in OTP's
internal weight units, which are roughly equivalent to seconds.  Set this to a high
value to discourage transfers.  Of course, transfers that save significant
time or walking will still be taken.


## nonpreferredTransferPenalty (Integer)

An additional penalty added to boardings after the first when the transfer is not
preferred. Preferred transfers also include timed transfers. The value is in OTP's
internal weight units, which are roughly equivalent to seconds. Set this to a high
value to discourage transfers that are not preferred. Of course, transfers that save
significant time or walking will still be taken.
When no preferred or timed transfer is defined, this value is ignored.


## maxTransfers (Integer)

The maximum number of transfers (that is, one plus the maximum number of boardings)
that a trip will be allowed.  Larger values will slow performance, but could give
better routes. This is limited on the server side by the MAX_TRANSFERS value in
org.opentripplanner.api.ws.Planner.


## batch (Boolean)

If true, goal direction is turned off and a full path tree is built (specify only once)


## startTransitStopId (String)

A transit stop required to be the first stop in the search (AgencyId_StopId)


## startTransitTripId (String)

A transit trip acting as a starting "state" for depart-onboard routing (AgencyId_TripId)


## clampInitialWait (Long)

When subtracting initial wait time, do not subtract more than this value, to prevent overly
optimistic trips. Reasoning is that it is reasonable to delay a trip start 15 minutes to
make a better trip, but that it is not reasonable to delay a trip start 15 hours; if that
is to be done, the time needs to be included in the trip time. This number depends on the
transit system; for transit systems where trips are planned around the vehicles, this number
can be much higher. For instance, it's perfectly reasonable to delay one's trip 12 hours if
one is taking a cross-country Amtrak train from Emeryville to Chicago. Has no effect in
stock OTP, only in Analyst.

A value of 0 means that initial wait time will not be subtracted out (will be clamped to 0).
A value of -1 (the default) means that clamping is disabled, so any amount of initial wait
time will be subtracted out.


## reverseOptimizeOnTheFly (Boolean)

If true, this trip will be reverse-optimized on the fly. Otherwise, reverse-optimization
will occur once a trip has been chosen (in Analyst, it will not be done at all).


## boardSlack (Integer)


## alightSlack (Integer)


## locale (String)


## ignoreRealtimeUpdates (Boolean)

If true, realtime updates are ignored during this search.


## disableRemainingWeightHeuristic (Boolean)

If true, the remaining weight heuristic is disabled. Currently only implemented for the long
distance path service.
