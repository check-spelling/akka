# ActorSink.actorRef

Sends the elements of the stream to the given @java[`ActorRef<T>`]@scala[`ActorRef[T]`], without considering backpressure.

@ref[Actor interop operators](../index.md#actor-interop-operators)

## Dependency

This operator is included in:

@@dependency[sbt,Maven,Gradle] {
  symbol1=AkkaVersion
  value1="$akka.version$"
  group="com.typesafe.akka"
  artifact="akka-stream-typed_$scala.binary.version$"
  version=AkkaVersion
}

## Signature

@apidoc[ActorSink.actorRef](ActorSink$) { scala="#actorRef[T](ref:akka.actor.typed.ActorRef[T],onCompleteMessage:T,onFailureMessage:Throwable=&gt;T):akka.stream.scaladsl.Sink[T,akka.NotUsed]" java="#actorRef(akka.actor.typed.ActorRef,java.lang.Object,akka.japi.function.Function)" }

## Description

Sends the elements of the stream to the given `ActorRef`.
If the target actor terminates the stream will be canceled.
When the stream is completed successfully the given `onCompleteMessage`
will be sent to the destination actor.
When the stream is completed with failure a the throwable that was signaled
to the stream is adapted to the Actors protocol using `onFailureMessage` and
then then sent to the destination actor.

It will request at most `maxInputBufferSize` number of elements from
upstream, but there is no back-pressure signal from the destination actor,
i.e. if the actor is not consuming the messages fast enough the mailbox
of the actor will grow. For potentially slow consumer actors it is recommended
to use a bounded mailbox with zero `mailbox-push-timeout-time` or use a rate
limiting operator in front of this `Sink`.

## Examples

TODO (in progress)
